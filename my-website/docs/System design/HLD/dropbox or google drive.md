Dropbox/Google Drive

Functional Requirements:
- download and upload files
- share
- realtime push to other users
- file consistency
- save versions of file
- ability to edit files offline
Note that dropbox scaled by making their own block storage (used to use s3, exabytes of data)
Real-time editing, text collaboration not included
Capacity Estimates:
- Files up to 1 gb
- Write based system (read write ratio of 1:1)

- split files into 4mb chunks for fast upload and diffing (what does hadoop use?)
- 500 million total users, 100 million per day, 200 files per user, 100kb on average per
file=10petapytes
- websockets for active connections
API Endpoints:
- Upload(userId, fileId, chunks)
- Download(fileId, localChunks) returns chunk URLs not yet on local machine (can use
merkle tree to track diffs between huge stores of data can be useful), list of hashes of
chunks is sufficient
- AddUser(userId, fileId, permissions)
Database Schema:
- store metadata, splitting files into chunks
- users table, file ids with names, associate for a given version file, which chunks
correspond
- ACID compliance
- Replication and partitioning -
- Cassandra doesn’t work because last write wins (leaderless), single leader replication,
sql config is the way to go
- Users (userId, email, passwordHash), Files (fileId, path), FileUsers (userId, fileId),
FileVersionChunks (fileIld, version, chunkHash), Chunks (chunkHash, s3Url, fileId) -
consistent hashing for data locality (all the metadata for a given chunk is on the same
machine, everything for a given file should be on the same shard)
- Avoid cross table joins
Architectural Design:
- Unnecessary components in other designs:
- All files should be split into chunks
- Client can look at old revision, and new changes, then say to itself here are the hashes
of all the chunks we last downloaded, here are the new chunks, only upload the new
ones. Then reach out to metadata server and actually commit the changes if this is the
newest version. If its not the newest version, client has to download the latest version
and merge it themself. This results in redundant uploads to s3 but thats ok, could have
background process that purges dead s3 uploads.
- Conflict resolution: how to determine if client is updating latest copy of that file? Reach
out to metadata sever and make sure there are no newer versions (could be solved with
2 phase commit, but that would add a lot of latency)
- Grokking says that “everytime a client wants to change a document, add it to a global
request queue”, not necessary because its so simple (could be http post request)
- They also say that everytime there is a change, all clients should be alerted, each client
should have a response queue, and server would send it to there. Not good because
constant updates. Instead, partition response queues by file ID - we know that all the

users aren’t going to have more than 200 files, so they would only keep 200ish
websockets.
- Store only 1 version of a given file - make users handle merges - in theory, we could
alternatively store both values as siblings (RIAK uses version vector), this isn’t git so who
cares, could just be linked list of versions
- Log based message queues to be consistent (also need to replicate for fault tolerance)
