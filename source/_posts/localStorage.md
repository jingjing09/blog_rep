---
title: localStorage
date: 2016-06-12 18:37:06
tags: html5
---
html5 提供了三种本地存储方式，分别是 Web Storage、Web SQL Database和 IndexDB.其中Web SQL Database目前IE和FF都不支持，IndexDB目前Safari和IOS均不支持，只有Chrome支持全部特性。本文主要讲述应用最为广泛的是Web Storage。
## 简述

Web Storage存储类似于object的键值对。其中，键(key)可以是strings或者integers，而值(value)只能是strings.

Web Storage包含如下两种机制：

- sessionStorage是在同源同窗口中始终存在的数据，也就是只要该浏览器窗口没有关闭，即使在该窗口中刷新当前页面或者打开同源的另一页面，数据依然存在。关闭窗口后，sessionStorage就会被销毁。同时独立打开不同的窗口，即使是同一页面，sessionStorage对象也不相同。
- localStorage和sessionStorage类似，最大的区别是生命周期不同，即使浏览器关闭也会持久保存在本地，除非手动清除。

## 可存放数据大小

一般浏览器中，每个域名下的localStorage、sessionStorage均可以存储5MB大小的数据。

## 同源

只有同源的页面之间才可以共享localStorage，同源同窗口才可以共享sessionStorage。


## 判断浏览器是否支持

在使用Web Storage之前有必要检测当前浏览器是否支持，

## 基本操作

## storage 事件

## 浏览器支持情况