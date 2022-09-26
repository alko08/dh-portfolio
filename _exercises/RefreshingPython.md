---
layout: page
title: Learning Python
description: Just some random functions and pieces of code with the purpose of refreshing python skills.
---
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5

This is plain text. 
* Item one
* Item two

[This is a link to a dog image](https://www.google.com/search?q=golden+retriever&source=lmns&bih=802&biw=1707&hl=en&sa=X&ved=2ahUKEwjTxKLUzab6AhXpD1kFHfMEDXcQ_AUoAHoECAEQAA)

This is a dog image.
<div>
    <img src="dog.JPG" width="200" alt="alt_text" align="left"/>
</div>

# Variables


```python
greeting = "Hello world!"
```


```python
print(greeting)
```

    Hello world!
    


```python
dog = "golden retriever"
print(dog)
```

    golden retriever
    


```python
dog = "Ginger"
print(dog)
```

    Ginger
    

# Strings


```python
ex_1 = "This is a string."
print(ex_1)
```

    This is a string.
    


```python
ex_2 = 'This is also a string.'
print(ex_2)
```

    This is also a string.
    


```python
ex_3 = 'One day I said, "Ginger come!" and she didn\'t come. That was the day we learned she was losing her hearing.'
print(ex_3)
```

    One day I said, "Ginger come!" and she didn't come. That was the day we learned she was losing her hearing.
    


```python
ex_4 = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
print(ex_4.lower())
```

    abcdefghijklmnopqrstuvwxyz
    


```python
"temp" == "temp"
```




    True




```python
"Temp" == "temp"
```




    False




```python
"temp".upper() == "TEMP"
```




    True




```python
first_name = "ada"
last_name = "lovelace"
fullname = first_name + " " + last_name
print(fullname)
```

    ada lovelace
    


```python
greeting = f"hello, {first_name} {last_name}"
print(greeting.title())
```

    Hello, Ada Lovelace
    

## Whitespace


```python
print("tab")
```

    tab
    


```python
print("\ttab")
```

    	tab
    


```python
print("Languages: \n-Greek\n-Latin\n-English")
```

    Languages: 
    -Greek
    -Latin
    -English
    


```python
str_rspace = "     string     "
print(str_rspace)
```

         string     
    


```python
print(str_rspace.rstrip().lstrip())
print(str_rspace.strip())
```

    string
    string
    

## Numbers


```python
# integers
238 + 4834
```




    5072




```python
238 - 4834
```




    -4596




```python
f = 238 / 8
type(f)
```




    float



## Lists


```python
subjects = ["Math", "English", "History", "Science", "Games"]
print(subjects)
```

    ['Math', 'English', 'History', 'Science', 'Games']
    


```python
print(subjects[0])
```

    Math
    


```python
print(subjects[-1])
```

    Games
    


```python
message = f"My most difficult subject is {subjects[1]}."
print(message)
```

    My most difficult subject is English.
    


```python
subjects[1] = "Computer Science"
```


```python
subjects.append("English")
```


```python
print(subjects)
```

    ['Math', 'Computer Science', 'History', 'Science', 'Games', 'English']
    


```python
subjects.insert(2, 'Algorithms')
```


```python
print(subjects)
```

    ['Math', 'Computer Science', 'Algorithms', 'History', 'Science', 'Games', 'English']
    


```python
del subjects[3]
print(subjects)
```

    ['Math', 'Computer Science', 'Algorithms', 'Science', 'Games', 'English']
    


```python
bad_subject = subjects.pop(-1)
print(bad_subject)
print(subjects)
```

    English
    ['Math', 'Computer Science', 'Algorithms', 'Science', 'Games']
    


```python
subjects.append("History")
print(subjects)
subjects.remove("History")
print(subjects)
```

    ['Math', 'Computer Science', 'Algorithms', 'Science', 'Games', 'History']
    ['Math', 'Computer Science', 'Algorithms', 'Science', 'Games']