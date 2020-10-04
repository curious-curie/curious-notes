---
title: LRU Cache Algorithm
date: "2020-09-01T22:40:32.169Z"
template: "post"
draft: false
slug: "lru-cache-algorithm"
category: "CS"
tags:
  - "Computer Architecture"
  - "Cache"
  - "CS"
description: "페이지 교체 알고리즘, 그리고 LRU 알고리즘 구현해보기"
socialImage: ""
---

# LRU Cache Algorithm 구현

### 페이지 교체 알고리즘

CPU가 계산을 할 때, 필요한 데이터가 페이지에 없다면 cache miss가 난다!

이 때는 보조기억장치로부터 데이터를 페이지로 옮겨온 후에 계산을 해야 함

페이지를 교체해야할 때, 어떤 페이지를 희생시켜야 할 것인가 ⇒ 페이지 교체 알고리즘

FIFO / LRU / LFU (Least Frequently Used) / OPT (OPTimal Page Replacement) 등이 있다 


### Least Recently Used: 가장 오랫동안 참조되지 않은 데이터를 제거하는 방법

- doubly linked list, hashMap 사용

```java
import java.util.HashMap;
import java.util.Map;

public class LRUCache {
	private Map<Integer, node> nodeMap;
	private int capacity;
	private node head;
	private node tail;

	private class node {

		private int key;
		private int value;
		private node prev;
		private node next;
		
		public node(int key, int value) {
			this.key = key;
			this.value = value;
			this.prev = null;
			this.next = null;
		}
	}

	public LRUCache(int capacity) {
		this.nodeMap = new HashMap<>();
		this.capacity = capacity;
		head = new node(0, 0);
		tail = new node(0, 0);
		head.next = tail;
		tail.prev = head;
	}

	private void remove(node node) {
		node.prev.next = node.next;
		node.next.prev = node.prev;
		nodeMap.remove(node.key);
	}

	private void insertToHead(node node) {
		this.head.next.prev = node;
		node.next = this.head.next;
		node.prev = this.head;
		this.head.next = node;
		nodeMap.put(node.key, node);
	}

	public int get(int key) {
		if(!nodeMap.containskey(key)) return -1;
		node getNode = nodeMap.get(key);
		remove(getNode);
		insertToHead(getNode);
	}

	public int put(int key, int value) {
		node newNode = new node(key, value);
		if (nodeMap.containsKey(key)) {
			node oldNode = nodeMap.get(key);
			remove(oldNode);
		} else {
			if(nodeMap.size() >= this.capacity) {
				node delNode = tail.prev;
				remove(delNode);
			}
		}
		insertToHead(newNode);
	}
}
```