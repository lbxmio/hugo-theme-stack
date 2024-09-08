+++
author = "zuimu"
title = "单个二极管状态分析"
date = "2022-11-06"
description = "判断是否导通和求输出电压Uo"
categories = [
    "模电"
]
tags = [
    "模电","期末"
]

+++

![](18.jpg)

# 单个二极管状态分析

![](1.png)

## 1.电路完整的话跳过1，电路不完整：

![screen-capture](115e9620ddd9ff26956c08d741a2e210.png)

<br/>

例如：![screen-capture](c75beeb619cae95df488a9104b9145e1.png)

变成了![screen-capture](25d40bbcf1ec00b6597b54dfdb04c9c4.png)

## 2.没什么好说的把二极管变成——阳极    断开    ——阴极

![screen-capture](6da13a537721e1a8490962c1d91edd0a.png)

## 3.分析两极电位

![screen-capture](043ea7123fab9750b2b0d72726ec7e7b.png)

例如：这个

![screen-capture](c8e20ecff8f3deeca64744e2a079ef65.png)

变成了

![screen-capture](fb538d39b650f38cd1f97f7ae7c4174a.png)

## 4.判断阳极减阴极是否大于导通电压（导通电压题目没说就是0）

阳-阴>Ud 二极管导通   

阳-阴<Ud 二极管截止

## 5.若二极管截止，跳过5

若二极管导通，则        <u>阳极        </u>    <u>阴极</u>      变成![screen-capture](b3ac9adf302235528014bfcd52366cf0.png)

3分析的电位作废

## 6.只分析Uo两端电压【用3】

输出电压=正电位-（负电位）

## 7.总结

![screen-capture](e02c8be6da5784babab045dbff574b0e.png)
