---
layout: post
author: me
title: "std::string 정리"
category: C++
---
C++ std::string 정리

## 특정 위치 문자 받기

{% highlight c++ %}
      char& at (size_t pos);
const char& at (size_t pos) const;
{% endhighlight %}

## 특정 문자 위치 받기

{% highlight c++ %}
string (1)	
size_t find (const string& str, size_t pos = 0) const noexcept;	

c-string (2)	
size_t find (const char* s, size_t pos = 0) const;	

buffer (3)	
size_t find (const char* s, size_t pos, size_type n) const;

character (4)	
size_t find (char c, size_t pos = 0) const noexcept;
{% endhighlight %}

## 특정 문자 삭제

{% highlight C++ %}
sequence (1) 
string& erase (size_t pos = 0, size_t len = npos);

character (2) 
iterator erase (const_iterator p);

range (3) 
iterator erase (const_iterator first, const_iterator last);
{% endhighlight %}

sequence는 시작 위치와 길이 값을 받는다. 길이의 기본값은 npos, 'string이 끝날 때까지'이다. <br>
만약 다음과 같은 코드라면

{% highlight C++ %}
string str = "cat is most adorable animal";
str.erase(7);
cout << str << endl; // cat is
{% endhighlight %}

7 이하의 문자는 모두 삭제된다. <br>
character는 특정 위치값을 받고, <br>
range는 시작 위치값과 끝나는 위치값을 받는다.

## 공백포함 한 줄 받기

{% highlight C++ %}
string str;
getline(cin, str);
{% endhighlight %}

## 문자 이스케이프

{% highlight C++ %}
//Code
cout << "\\" << endl;
cout << "\"" << endl;

//Ouput
\
"
{% endhighlight %}

출처 [string]

[string]: http://www.cplusplus.com/reference/string/string/

