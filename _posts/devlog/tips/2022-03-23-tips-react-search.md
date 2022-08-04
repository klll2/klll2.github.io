---
layout: post
title: '[React] 검색 기능 구현 하는법'
subtitle: '[React] 검색 기능 구현 하는법'
category: devlog
tags: tips react
image:
  path:    /assets/img/reactlogo.png
---

어떠한 페이지 혹은 프로그램에 거의 필수적으로 들어가는 기능이 있다. 바로 검색 기능!  
지금은 크게 어려움이 없지만, 처음 공부하던 시절에는 많이 어려웠었고, 필요한 사람이  
있을 수 있으니 다시 한번 되짚어 보고자 한다.  

<!-- more -->

* this ordered seed list will be replaced by the toc
{:toc}  

## 구현 시 필요한 함수와 로직  
---  
검색 기능을 구현하기 위해서는 `Array.prototype.filter()` 라는 배열함수가 필요하다.  
전체적인 로직은 인풋에서 받은 값과 데이터의 값들을 비교하여 일치 하는 값들만 1차적으로 거르고  
2차적으로는 거른 값에 `Array.prototype.map()`으로 다시 데이터를 뿌려주는 것이다.  

## 코드 작성  
---  
* 어떠한 데이터가 들어가 있는 json 파일을 "sampleData" 라는 이름으로 불러왔다고 가정한다.  
* 우리가 입력하는 값을 받아오는 인풋의 state는 "userInput" 이라고 정하겠다.  
* 검색기능을 하고 ui를 만들어주는 함수의 이름은 "searchList" 라고 정해주겠다.  
```react
// file: "search.js"
const searchList = () =>{
  return <></>
}
```  


* 1차적으로 먼저 걸러줄 매소드를 변수로 만들어 놓기  
```react
// file: "search.js"
const searchList = () =>{
  const filtered = sampleData.filter((itemList) => {
    return itemList.name.toUpperCase().includes(userInput.toUpperCase());
  return <></>
}
```  

sampleData에 filter함수를 넣어 itemList의 안에(includes() 사용) 내가 입력한 값과  
일치하는 값만 반환해준다. 여기에서 `toUpperCase()` 를 양쪽에 써준이유는 기준이 되는 데이터와  
내가 입력한 값을 동일하게 대문자로 변경해주어서 대문자, 소문자 구문없이 다 검색이 되게끔 한 것이다.  

* 1차에서 걸러진 값을 새로 map으로 뿌려주기  
```react
// file: "search.js"
const searchList = () =>{
  const filtered = sampleData.filter((itemList) => {
    return itemList.name.toUpperCase().includes(userInput.toUpperCase());
  return (
    <div className="cardList">
      {filtered.map((itemList) => {
        return <Card key={itemList.id} {...itemList} />;
      })}
    </div>
}
```  

1차에서 걸러진 값을 저장한 변수 "filtered" 를 `Array.prototype.map()` 함수로  
뿌려준다. 이렇게 하면 이미 1차에서 검색한 값을 걸러주었기때문에 그 값을 가지고 새로 리스트화 한다.  

## 검색 기능 구현 결과  
---  
컴포넌트 재사용 연습으로 구현해본 몬스터라는 것으로 검색 기능을 구현해 보았다.  

![사진1](/assets/img/tips/2022-03-25-react-search/2022-03-25-search.gif)  

