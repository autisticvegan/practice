


      class BookFilter

2      {

3          virtual bool apply(Book) = 0;

4      };

5      class TitleFilter : public BookFilter

6      {

7      private:

8          std::string m_title;

9      public:

10          TitleFilter(std::string title)

11         {

12              m_title = title;

13         }

14          override bool apply(const Book& book)

15         {

16             if (Book.title.find(m_title) != std::string::npos)17

17                  return true;    

18

19              return false

20          }

21      };

22      typedef enum

23      {

24          Big,

25          Medium,

26          Small

27      } BookSize;

28      class BookSizeFilter : BookFilter

29      {

30      private:

31          BookSizeFilter(BookSize desiredSize)

32          {

33             m_desiredSize = desiredSize;

34          }

35          override bool apply(const Book& book)

36          {

37              unsigned int minPages = 0;

38              unsignedint maxPages = 0;

39        

40              switch m_desiredSize

41              {

42              case Big:

43                  minPages = 0;

44                  maxPages = 100;

45              case Medium:

46                  minPages = 101;

47                  maxPages = 500;

48              case Small:

49                  minPages = 501;

50                  maxPages = std::UINT_MAX;

51              }

52              return (Book.pageCount >= minPages) && (Book.pageCount < maxPages);

53          }

54      }

55      bool BookPassesFilters(const Book& book, std::List<BookFilter>& filters)

56      {

57          for (BookFilter filter : filters)

58          {

59              if (!filter.apply(book))

60                  return false;

61          }

62          return true;

63      }

64      std::set<Book> FilterBooks(std::List<Book> bookList, std::List<BookFilter>& filters)

65      {

66          std::set<Book> rval;

67          for (Book book : bookList)

68          {

69              if (bookPassesFilters(book, filters))

70                  rval.push_back(book);

71          }

72          return rval;

73      }

 