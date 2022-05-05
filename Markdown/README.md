# Markdown

## Markdown을 공부해야 되는 이유
개발자가 자신의 코드를 저장소에 저장할때 코드의 역할과 사용법이 README.md 파일에 작성된다. 코드 자체도 정말 중요하지만 코드를 상대방에게 효과적으로 전달하고 마케팅하기 위한 README.md 파일도 중요하다고 생각한다. 따라서 Markdown을 공부해야 된다.

## Markdown 문법

### 1. 제목 (Header)

```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

### 2. 선 (Line)

```markdown
***
---
```

***
___

### 3. 강조 (Emphasis)

```markdown
default *italic* **bold** ~~strikethrough~~
```

default *italic* **bold** ~~strikethrough~~

### 4. 인용문 (Quote)

```markdown
> qoute 1
> > quote 2
```

> qoute 1
> > quote 2

### 5. 목록 (List)
#### 순서가 있는 목록 (Ordered List)
 ```markdown
 1. First
 2. Second
 3. Third
 ```

 1. First
 2. Second
 3. Third

#### 순서가 없는 목록 (Unordered List)
```markdown
* Bullet 1
- Bullet 2
    + Bullet 2-1
+ Bullet 3
    - Bullet 3-1
        * Bullet 3-2
```

* Bullet 1
- Bullet 2
    + Bullet 2-1
+ Bullet 3
    - Bullet 3-1
        * Bullet 3-2

### 6. 코드 (Code)
#### 인라인 (Inline)
```markdown
`code` paragraph
```
`code` paragraph
#### 블록 (Block)
<pre>
<code>
paragraph
```
code block
```
paragraph
</code>
</pre>

paragraph
```
code block
```
paragraph

GitHub에서는 첫번째 코드블럭코드(```) 뒤에 사용하는 언어를 사용하여 문법을 강조할 수 있다.
<pre>
<code>
```Python
print("Hello, world!")
```
</code>
</pre>

```Python
print("Hello, world!")
```

<pre>
<code>
```Java
public class Main {
 
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```
</code>
</pre>

```Java
public class Main {
 
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

### 7. 링크 (Link)
```markdown
https://github.com

[GitHub](https://github.com) 
```
https://github.com

[GitHub](https://github.com) 

### 8. 이미지 (Image)
```markdown
![yaktocat](https://octodex.github.com/images/yaktocat.png)
```

![yaktocat](https://octodex.github.com/images/yaktocat.png)

사이즈를 조절하기 위해서는 `<img src="" width="" height=""></img>`를 사용해야 한다.
```markdown
<img src=https://octodex.github.com/images/yaktocat.png width="300" height="300"></img>
```

<img src=https://octodex.github.com/images/yaktocat.png width="300" height="300"></img>

### 9. 표 (Table)
```Markdown
|Description1|Description2|Description3|Description4|
|--|:--|--:|:--:|
|default|right|left|center|
```

|Description1|Description2|Description3|Description4|
|--|--:|:--|:--:|
|default|right|left|center|

## 참고 (Reference)
* [YouTube 드림코딩](https://www.youtube.com/watch?v=kMEb_BzyUqk&ab_channel=%EB%93%9C%EB%A6%BC%EC%BD%94%EB%94%A9by%EC%97%98%EB%A6%AC)

* [GitHub Guides](https://guides.github.com/features/mastering-markdown/)

* [마크다운 작성법](https://gist.github.com/ihoneymon/652be052a0727ad59601#-%EC%88%9C%EC%84%9C%EC%9E%88%EB%8A%94-%EB%AA%A9%EB%A1%9D%EB%B2%88%ED%98%B8)
