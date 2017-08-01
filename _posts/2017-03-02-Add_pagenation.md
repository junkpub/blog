---
layout: post
title:  "블로그 포스트 pagination 추가"
date:   2017-03-02 18:21:32 +0900
categories: jekyll
tags: jekyll liquid
---
테스트해보니 포스트가 많아지면 자동으로 페이지로 관리되지 않는 듯 하다. 뭐... 당연한 결과인데 너무 큰 기대를 한건가?;;;

그래서 `pagination`을 추가하기로 결정. 일단 `pagination`을 사용하려면 `_config.yml`을 사용해야 하는 듯. `_config.yml`에 다음을 추가하면 된다.
{% highlight liquid %}
paginate: 10
{% endhighlight %}
위 처럼 설정하게 되면 한 페이지의 10개의 포스트를 보여주게 된다. 난 그냥 무난하게 10개로 결정.

`_config.yml`만 수정한다고 바로 적용되는 것이 아니고 `paginator` 글로벌 변수를 적용해야한다. 주의할 것은 `index.html`만 가능하다는 점.

paginator를 사용하기 위해서는 site.posts를 사용하는 것이 아니라 paginator.posts를 사용해야 한다. 해당 페이지의 링크를 클릭하게 되면 `/page3`과 같은 주소가 붙게 되는데 `paginator.page`가 1인 경우에는 `/`을 사용한다는 것을 염두해두도록 한다.

{% highlight liquid %}
{% raw %}
<div class="pagination">
    {% if paginator.previous_page %}
        {% if paginator.previous_page == 1 %}
        <a href="/">&laquo;</a>
        {% else %}
        <a href="/page{{ paginator.previous_page }}">&laquo;</a>
        {% endif %}
    {% else %}
    <a>&laquo;</a>
    {% endif %}

    {% for page in (begin..end) %}
        {% if page == paginator.page %}
        <a class="active">{{ page }}</a>
        {% else %}
            {% if page == 1 %}
            <a href="/">{{ page }}</a>
            {% else %}
            <a href="/page{{ page }}">{{ page }}</a>
            {% endif %}
        {% endif %}
    {% endfor %}

    {% if paginator.next_page %}
    <a href="/page{{ paginator.next_page }}">&raquo;</a>
    {% else %}
    <a>&raquo;</a>
    {% endif %}
</div>
{% endraw %}
{% endhighlight %}

이제 포스트 리스트 하단에 페이지를 넘길 수 있도록 `pagination`이 생성 됐다(`css`가 없어서 거지같아 보이는건 신경쓰지 말도록 하자... -_-ㅋ). 그런데 위의 코드는 페이지 리스트가 무한정 늘어나도록 되어 있다. 조금 더 수정을 해보자. 페이지 리스트는 5개 까지만 나오게 하고 싶다. 예를 들자면 (1 2 3 4 5)가 나오고 5에서 다음 페이지로 넘어가게 되면 (6 7 8 9 10)로 바뀌는 형태. 12번째 줄을 주목해보자. 1페이지부터 마지막 페이지까지 반복하겠다는 의미인데 이 부분을 수정하면 될 듯 하다. `1`과 `paginator.tatal_pages`대신에 다른 시작과 끝을 정해주면 된다.

{% highlight liquid %}
{% raw %}
{% assign begin = paginator.page | minus: 1 | divided_by: page._shownpages | times: page._shownpages | plus: 1 %}
{% assign tmpend = begin | plus: page._shownpages %}
{% if paginator.total_pages < tmpend %}
{% assign end = paginator.total_pages %}
{% else %}
{% assign end = tmpend %}
{% endif %}
{% endraw %}
{% endhighlight %}

`begin`과 `end`를 계산했다. 설명은 귀찮으니 패스;;;. 빌어먹을 `liquid`언어로 사칙연산하는거 겁나 빡세네ㅠㅠ. 나중에 혹시나 다룰 기회가 있으면 그때 정리해야지. 저렇게 사용하는게 맞는지도 모르겠다 지금은 솔직히 ㅋㅋㅋ. 급한데로 막 가져다 쓴거라. 이제 위의 예제에서 12번째 줄을 다음 처럼 수정만 하면 된다.
`liquid` 참고사이트 https://help.shopify.com/themes/liquid

{% highlight liquid %}
{% raw %}
{% for page in (begin..end) %}
{% endraw %}
{% endhighlight %}

마지막으로 css를 추가해서 마무리~
음... 아주 맘에 들지는 않지만 그래도 일단은 만족한다.
