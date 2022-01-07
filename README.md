# CodeView
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/343df315aa3b40e09e6e98cf32ff8468)](https://app.codacy.com/gh/AmrDeveloper/CodeView?utm_source=github.com&utm_medium=referral&utm_content=AmrDeveloper/CodeView&utm_campaign=Badge_Grade_Settings)
[![CodeFactor](https://www.codefactor.io/repository/github/amrdeveloper/codeview/badge)](https://www.codefactor.io/repository/github/amrdeveloper/codeview)
![Build](https://github.com/amrdeveloper/codeview/actions/workflows/build.yml/badge.svg)
[![Min API Level](https://img.shields.io/badge/API-%2B14-brightgreen)]()
![Maven Central](https://img.shields.io/maven-central/v/io.github.amrdeveloper/codeview?color=green)
[![Jitpack Version](https://jitpack.io/v/AmrDeveloper/CodeView.svg)](https://jitpack.io/#AmrDeveloper/CodeView)

Android Library to make it easy to create your CodeEditor or IDE for any programming language 
even for your programming language, just config the view with your language keywords and other attributes
and you can change the CodeView theme in the runtime so it's made it easy to support any number of themes, 
and CodeView has AutoComplete and you can customize it with different keywords and tokenizers.

## Demo
<p align="center">
  <img src="media/python_demo.gif" alt="animated" width="23%"/>
  <img src="media/java_demo.gif" alt="animated" width="23%"/>
  <img src="media/golang_demo.gif" alt="animated" width="23%"/>
  <img src="media/snippets_demo.gif" alt="animated" width="23%"/>
  <img src="media/multi_comments_demo.png" alt="animated" width="242" height="480"/>
  <img src="media/error_line_demo.png" alt="animated" width="242" height="480" />
</p>

- Main Features
  - Can support any programming language you want
  - Can support AutoComplete and customize it with different tokenizers and design
  - Can support any theme you want and change it in the runtime
  - Syntax Highlighter depend on your patterns so you can support any features like TODO comment
  - Can support errors and warns with different colors and remove them in the runtime
  - Can change highlighter update delay time
  - Support Code snippets and change it in the runtime
  - Support optional Line Number with customization
  - Support Auto indentation with customization
  - Support highlighting matching tokens
  - Support replace first and replace all matching tokens

##### If you use CodeView in an interesting project, I would like to know

### Add CodeView to your project 
#### Add CodeView from Maven Central

```gradle
dependencies { 
    implementation 'io.github.amrdeveloper:codeview:1.2.1'
}
```

<details>
  <summary>Or Add CodeView from Jitpack.IO</summary>
  
  ##### Add it to your root build.gradle
  ````gradle
  allprojects {
      repositories {
          ...
          maven { url 'https://jitpack.io' }
      }
  }
  ````

  ##### Add the dependency
  ````gradle
  dependencies { 
      implementation 'com.github.AmrDeveloper:CodeView:1.2.1'
  }
  ````
</details>

#### Documentation
CodeView is based on AppCompatMultiAutoCompleteTextView

Add CodeView on your xml 

```xml
<com.amrdeveloper.codeview.CodeView
    android:id="@+id/codeView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/darkGrey"
    android:dropDownWidth="@dimen/dimen150dp"
    android:dropDownHorizontalOffset="0dp"
    android:dropDownSelector="@color/darkGrey"
    android:gravity="top|start" />
```

Initialize CodeView

```java
CodeView codeView = findViewById(R.id.codeview);
```

Clear all patterns from CodeView

```java
codeView.resetSyntaxPatternList();
```

Add Patterns for your language, you can add any number of patterns

```java
codeView.addSyntaxPattern(pattern, Color);
```

Or add all patterns as an Map Object

```java
codeView.setSyntaxPatternsMap(syntaxPatterns);
```

Highlight the text depend on the new patterns
  
```java
codeView.reHighlightSyntax();
```

Add error line with dynamic color to support error, hint, warn...etc

```java
codeView.addErrorLine(lineNumber, color);
```

Clear all error lines

```java
codeView.removeAllErrorLines();
```

Highlight the errors depend on the error lines

```java
codeView.reHighlightErrors();
```
  
Add Custom AutoComplete Adapter

```java
//Your language keywords
String[] languageKeywords = .....
//List item custom layout 
int layoutId = .....
//TextView id on your custom layout to put suggestion on it
int viewId = .....
//Create ArrayAdapter object that contain all information
ArrayAdapter<String> adapter = new ArrayAdapter<>(context, layoutId, viewId, languageKeywords);
//Set the adapter on CodeView object
codeView.setAdapter(adapter);
```

Add Custom AutoComplete Adapter that support keywords and Snippets

```java
List<Code> codes = new ArrayList<>();
codes.add(new Snippet(..., ..., ...));
codes.add(new Keyword(..., ..., ...));

//Your language keywords
String[] languageKeywords = .....
//List item custom layout
int layoutId = .....
//TextView id on your custom layout to put suggestion on it
int viewId = .....

CodeViewAdapter codeAdapter = new CodeViewAdapter(context, layoutId, viewId, codes);
codeView.setAdapter(codeAdapter);
```

Add Custom AutoComplete Tokenizer
    
```java
 codeView.setAutoCompleteTokenizer(tokenizer);
```

Set highlighter update delay

```java
codeView.setUpdateDelayTime();
```

Enable/Disable highlight the code while the text is changing

```java
codeView.setHighlightWhileTextChanging(enableHighlighter);
```

Enable/Disable line number

```java
codeView.setEnableLineNumber(enableLineNumber);
```

Set line number text color

```java
codeView.setLineNumberTextColor(Color.GREY);
```

Set line number text size

```java
codeView.setLineNumberTextSize(size);
```

Set Tab length

```
codeView.setTabLength(4);
```

Enable/Disable Auto Indentation

```
codeView.setEnableAutoIndentation(enableIndentation);
```

Set Indentations Starts

```
codeView.setIndentationStarts(indentationStart);
```

Set Indentations Ends

```
codeView.setIndentationEnds(indentationEnds);
```

Change the matching highlighter color

```
codeView.setMatchingHighlightColor(color);
```

Get and save all the tokens that matching regex

```
List<Token> tokens = codeView.findMatches(regex);
```

Find and highlight the next matching token, returns null if not found

```
Token token = codeView.findNextMatch();
```

Find and highlight the previous matching token, returns null if not found

```
Token token = codeView.findPrevMatch();
```

Clear all matching highlighted token

```
codeView.clearMatches();
```

Replace the first string that matching regex with other string

```
codeView.replaceFirstMatch(regex, replacement);
```

Replace all strings that matching regex with other string

```
codeView.replaceAllMatches(regex, replacement);
```

#### For real examples on how to use CodeView check the example app
