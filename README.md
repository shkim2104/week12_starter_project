# OSS Week 11 — React Course Manager (Student Starter)

React + Vite 기반 학생 배포용 Sample Project입니다. **조회와 삭제는 완성**, 등록 및 완료 변경은 학생이 직접 구현하도록 `TODO`로 남겨두었습니다.

## Github && Vercel url
Vercel : https://week11-ebon.vercel.app/
Github : https://github.com/shkim2104/week11

## 실행 방법
Node.js 20.19+ 또는 22.12+ 권장.

```bash
npm install
npm run dev
```

브라우저에 표시되는 Local URL에 접속하세요. 빌드 테스트: `npm run build`.


실행결과
![실행결과](./1.png)

## 소스 구조

- app.jsx : 헤더 풋터를 읽어오고 화면에 띄우는 역할
- CourseItem.jsx : 부모 CourseList.jsx로 부터 상속 받은 아이로 CourseList.jsx에 있는 함수들을 불러와 사용하고, 과목과 과목제거 체크 박스를 보여주는 역할을 한다.
- CourseList.jsx: 과목 배열을 불러오고 자식  CourseItem.jsx에 함수 여러함수를 내려주고 화면에 현재 진행중인 목록과 개수를 보여주고 서로 props로 구현된  상태입니다.

- component와 props의 관계
    - 부모인 courselist가 자식인 courseitem에 정보를 주고 그럼 자식인 애는 함수에서 요청을 보내는 구조로서 코드에서는 새과목을 추가할때 그렇게 받아서 새로운 배열로 데이터를 추가했습니다.
- useState && event 분석
    - useState : 일반 변수와 state의 차이는 react가 아냐 모르냐 라는 것이 차이점입니다. react는 state를 알아차리기 때문에 우리가 실시간으로 코드를 바꾸면 곧 바로 실제 페이지에 바로 적용이 되어서 편리하다는 장점이 있습니다.

    - event 분석 : delete를 눌렀을때 ondelete를 자기 번호와 같이 누르고 , handleDelete가 실행 되면서 alert로 알람을 가고 확인한뒤 filter로 그 번호가 아닌 것만 남긴 데이터를 만들어서 react에 보내서 곧 바로 react가 실행되어서 페이지가 바뀌게 됩니다.

- 주요 코드
    - handleAdd
        -  function handleAdd(event) {
            event.preventDefault();

            if(!newName.trim()) {
            alert('과목명을 입력하세요.');
            return;
            }
            setCourses(previous => {
            const newCourse = {
                id: previous.length > 0 ? Math.max(...previous.map(course => course.id)) + 1 : 1,
                name: newName.trim(),
                category: '선택', 
                completed: false
            };
            return [...previous, newCourse];
            });
            setNewName('');
        }
        
        위코드에서 처음에 빈 배열인지를 확인 후 새 과목코드를 만듭니다. 다음으로 지금 존재하는 id 에서 가장 큰 번호에 + 1를 합니다. 안 그러면 나중에 존재하는 번호랑 겹칠 수 있기 때문입니다. 그리고 새 입력창에 있던 내용을 다시 초기화해서 다음에 추가로 과목을 추가할때 바로 적을 수 있게끔 입력창의 값도 초기화 합니다.

    - handleToggle
        - function handleToggle(id) {
            setCourses(previous => previous.map(course => {
            if(course.id === id) {
                return { ...course, completed: !course.completed };
            }
            return course;  
            }));
          } 

          위 코드에서 id를 map으로 확인하여서 check박스를 누른 것을 계속해서 하나씩 보면서 확인하여 누른 거랑 id가 같다면 complete로 변경하여 react에 값이 전송되어서 check 박스에 확인이 됩니다.


## 수정한 데이터 
- 수정한 최종 화면 상태
![css-1-full-page](./screenshots/css-1-full-page.png)

- index.html에 title 부분과 태그 와 저만의 스타일로 배경을 바꿧습니다
![css-2-header-topline-tag](./screenshots/css-2-header-topline-tag.png)


- 초기 데이터의 값을 저의 미래를 위한 과목을 듣고 싶은 과목을 희망사항으로 추가해 초깃값을 변경하였습니다.
![css-4-course-rows-check-category](./screenshots/css-4-course-rows-check-category.png)

## Weekly Review

- 새롭게 배운 내용 3가지
    - 1. previous를 setCourse 안에서 써야 하는데 그것을 바깥을 옮겨서 코드가 오작동을 일으켜서 몸소 깨우쳤습니다.
    - 2. state만 바꾸었ㄴ느데 통게와 취소선 체크박스 표시가 자동으로 바꾸어 진것이 react가 바로 반응하여 볼 수 있다는 것이 엄청난 장점이라는 것을 배웠습니다.
    - 3. 상속 구조로 불러와서 함수를 호출하여 사용할 수 있는 것을 배웠습니다.
- 어려웠던 점과 해결 방법
    - 데이터를 새로 추가할 배열을 만들때 어떻게 만들어야 할지 몰라서 막막했는데 경우의 수를 줄여서 코드를 하나씩 다 해봐서 코드를 만들었습니다.
- AI 활용 내용 및 느낀 점
    - ai로 배운 삼항 연산자로 코드를 하는 것을 해봤는데 그냥 if문 쓰겠습니다.

    - 항상 코드를 수정하고 스크린샷을 안찍어서 ai한테 내가 수정한 것들 다 스크린샷 찍어서 파일에 저장해달라고 했습니다.
        - ❯ 그럼 그 지금 readme에 ##수정한 데이터 부분에 사진만 넣어줄래? 그럼 내가 그 밑에다가 고친부분에 대한 자세한 설명 적게 