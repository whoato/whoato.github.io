---
layout: post
author: me
title: "jekyll css 적용 안됨"
category: jekyll
---
jekyll step-by-step을 따라서 고생고생 끝에 빌드하고 push했는데 css가 적용이 안됐다.<br>
분명 시키는대로 다 했고 로컬 서버 테스트에서는 잘 보였는데..<br>
Github으로 올리니까 하나도 적용이 안되었다.

대체 무슨 이유인가 싶어서 찾아보니 css를 불러오는 주소가 절대주소로 적혀있었다.<br>
튜토리얼에서도 절대주소로 적혀있고 아무런 말이 없었는데 -_-;;<br>
아무튼 찾아낸 해결법은 다음과 같다.

1. _config.yml에서 url 입력란에 자신의 블로그 주소를 써넣는다.

{% highlight yml %}
url: "https://<your_id>.github.io"
{% endhighlight %}

{:start="2"}
2. css를 불러오는 부분에서

{% highlight html %}
<link rel="stylesheet" href="/assets/css/styles.css">
{% endhighlight %}

{:start="3"}
3. 이 부분을 아래 코드처럼 바꿔주어야 한다.

{% highlight html %}
<link rel="stylesheet" href="{% raw %}{{ root_url }}{% endraw %}/assets/css/styles.css">
{% endhighlight %}

