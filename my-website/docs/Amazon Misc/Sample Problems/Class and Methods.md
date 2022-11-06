
Track heard utterances/phrases and Return the top 100 utterances in descending order of popularit

- Can use Redis (top k)
- Can use heaps


```

type Utterance struct {

    metadata ...
    wave ...
    word 
    
}

type UtterancesRanker struct {

    utters []Utterance
    ranking algo ...
    

}
```