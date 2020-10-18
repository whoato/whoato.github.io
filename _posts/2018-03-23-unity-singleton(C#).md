---
layout: post
author: me
title: "Unity Singleton(C#)"
category: [Unity, C#]
---
유니티 C#으로 구현한 싱글톤 클래스

{% highlight C# %}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GenericSingletonClass<T> : MonoBehaviour where T : Component {

	private static T _instance;
	public static T Instance {
		get	{
			if (_instance == null) {
				_instance = FindObjectOfType<T> ();
				if (!_instance) {
					GameObject container = new GameObject ();
					container.name = typeof(T).Name;
					_instance = container.AddComponent<T> ();
				}
			}
			return _instance;
		}
	}

	public virtual void Awake() {
		if (_instance == null) {
			_instance = this as T;
			DontDestroyOnLoad (this.gameObject);
		} else {
			Destroy (gameObject);
		}
	}
}
{% endhighlight %}