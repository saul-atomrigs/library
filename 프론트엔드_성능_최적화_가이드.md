# 프론트엔드 성능 최적화 가이드
![image-book](https://contents.kyobobook.co.kr/sih/fit-in/458x0/pdt/9788966263745.jpg)

# 제 2 장

### **컴포넌트 사전 로딩 & 이미지 사전 로딩**

- 사용자가 버튼 위에 마우스를 올려놨을 때(`onMouseEnter`), 사전 로딩 시작하기
    
    ```jsx
    const handleMouseEnter = () => {
     const component = import('./components/ImageModal)
    }
    
    return (
     <button onMouseEnter={handleMouseEnter} />
    )
    ```
    
- 최초에 페이지가 로드되고 모든 컴포넌트의 마운트가 끝났을 때, 사전 로딩 시작하기
    
    ```jsx
    useEffect(() => {
     const component = import('./components/ImageModal)
    }, [])
    ```
    

외부 라이브러리를 사용한다는건 해당 라이브러리의 사이즈만큼 최종 번들 크기가 커진다

### 브라우저 렌더링 과정

(DOM + CSSOM) → 렌더 트리 → 레이아웃 → 페인트 → 컴포지트

### 리플로우와 리페인트

“다시” 그려야 할 때

- 리플로우: 브라우저 렌더링 과정을 모두 거친다. 따라서 더 느릴 수 밖에.
- 리페인트: 색생만 다시 칠해야 할 때. (브라우저 렌더링 과정에서 **레이아웃 만 제외하고 모두 재실행)**

피하는 방법: (`width` , `height`, `color`  대신) `transform` , `opacity` 속성 사용하기
