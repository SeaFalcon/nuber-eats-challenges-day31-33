# nuber-eats-challenges-day31-33

<details>
  <summary>
  Day 29-30 정답해설
  </summary>

1. authLink
- 백엔드에서 role기반(Host, Listener, Any)의 권한부여를 작업했기 때문에 클라이언트에서도 마찬가지로 서버에게 유저 정보에 대해 알려줘야 합니다.
- ![](https://i.ibb.co/mDLx8mx/concat-auth.png)
- 위의 그림처럼 authLink에 setContext를 넘겨줘서 기존의 httpLink과 연결시켜주면 됩니다.
- 위의 코드에 대해 너무 고민하지 마세요. apollo client에서 저렇게 사용하는 것이므로, 그냥 따라 주면 됩니다. Link는 여러가지 종류가 있습니다. 그 중의 하나인 Context Link를 사용한 것입니다.
- 위 코드와 같이 설정을 해주면 이제 request header에는 x-jwt라는 키값에 인증 토큰이 들어가게 되고, 서버에서는 위 토큰을 받아서 유저 정보를 파악할 수 있게 됩니다. 그래서 롤 기반 권한부여를 구현할 수 있게 됩니다.
2. 팟캐스트 & 에피소드 렌더링
- apollo client의 useQuery 훅을 이용하면 쉽게 구현이 가능합니다.
- useQuery는 함수는 쿼리어(gql)과 옵션 값을 입력 받아, 서버에 전달하여 query 문에 대한 결과 값을 가져옵니다. useQuery가 리턴해주는 값을 아주 많습니다. 그중에서 우리가 강의에서 많이 사용한 것은, data, loading, errors였습니다.
- 그 외에도 refetch와 fetchMore 등은 instagram clone 코스(v3)에서도 많이 다룹니다. 우버이츠 클론 강의에서도 apollo client 캐쉬에 대해서 다뤘지만, 인스타그램 클론 코스에서 조금 더 심도 있게 다룹니다. refetch와 fetchMore도 알아 두시면 좋을 것 같습니다.
- useQuery의 결과 값으로 솔루션에서는 podcast의 배열 값을 받습니다. 그 배열값을 javascript의 Array.map을 이용하여 렌더링 합니다. 리액트를 다루신 분이면 충분히 많이 사용했던 방법일 것이기 때문에 특별한 설명은 생략하겠습니다.

###결론
useQuery를 이용하여 server에 data fetching을 하여 렌더링하는 과정을 구현하는 과제였습니다. 리액트에 대한 기본과 useQuery 사용법만 알면 충분히 쉽게 구현할 수 있는 과제였습니다.
</details>

### UI Testing Time!
- 오늘의 강의: 우버 이츠 클론코딩 강의 #18.0 - #18.11 (21.09.22 ~ 24)
- 오늘의 과제: 위의 강의를 시청하신 후, 아래 코드 챌린지를 제출하세요.

### Code Challenge
- 오늘은 지금까지 만든 페이지(스크린)와 컴포넌트들을 테스트 할 차례입니다.
- 현재 테스트 커버리지는 아래 그림과 같은 상태입니다. 이번 3일 동안의 목표는 아래 커버리지 상태를 100%로 만드는 것입니다(최대한, 할 수 있는 만큼).
- ![](https://i.imgur.com/N8mNGg8.png)

- 블루프린트에서 episodes.spec.tsx, podcasts.spec.tsx, login.spec.tsx and create-account.spec.tsx 파일들을 보실 수 있습니다. 이 파일들은 이미 mock-apollo-client설정이 되어 있습니다.
- 먼저 샌드박스에서 컴퓨터로 코드를 다운로드 하시고, npm i 한 후에 npm run test:coverage를 입력해보세요. 테스트 하려면 콘솔에 test:coverage를 입력하시면 됩니다.
- 제출은 코드 샌드박스 링크, 또는 깃헙 커밋 링크를 보내주시면 됩니다.



<details>
  <summary>
  Hint
  </summary>

- 백엔드에서도 다뤘던 유닛테스트입니다. 설정과 테스트 방법이 당연하지만 사뭇 다르기 때문에 강의 내용과 문서, 검색 등을 활용하시어 최대한 커버리지를 채우면 되겠습니다.
- 블루프린트에 웬만한 것들이 셋팅(test-utils.tsx)이 되어 있어서 테스트 설정에 대한 고민은 덜어두시고 쾌적하게 테스트 하시면 되겠습니다.
- 유닛테스트의 기본목적은 똑같기 때문에, 테스트하려는 스크린, 컴포넌트를 제외한 요소인 데이터 fetching 같은 것은 mocking 해야 합니다. jest의 mockResolvedValue 등을 이용하시면 됩니다.
- act나 waitFor를 잘 활용하셔야 합니다. mutation, query 같은 작업을 서버에 요청하는 작업이나 유저 입력을 mocking하는 부분, 렌더링 부분, state change 등에서 act 나 waitFor를 활용하지 않으시면 원하시는 테스트 결과가 나오지 않을 수 있습니다.
- apollo client를 이용하여 resolved value를 같은 것을 mocking하실 때, __typename에 주의하세요.
- react router dom과 같은 패키지들을 mocking할 때 주의하셔야 합니다. 전체 패키지 중에 일부만 mocking하는 부분이 강의에서 나오는데 참고바랍니다. 힌트: jest.requireActual
- handleSubmit 콜백함수 때문에 100% 커버리지 채우기는 어려울 수 있습니다.
</details>