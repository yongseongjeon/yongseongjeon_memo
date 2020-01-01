---
title: "읽기 좋은 코드가 좋은 코드다 [4/12]"
date: 2020-01-01 15:22:00 -0400
categories: 책 요약
---

## 핵심 아이디어
- 본인이 지은 이름을 "다른 사람들이 다른 의미로 해석할 수 있을까?"라는 질문을 던져보며 철저하게 확인해야 한다.

## 목차
  1. [여러 블록에 담긴 코드가 모두 비슷한 일을 수행하면, 실루엣이 동일해 보이게 만들어라](#여러-블록에-담긴-코드가-모두-비슷한-일을-수행하면,-실루엣이-동일해-보이게-만들어라)
  2. [코드 곳곳을 '열'로 만들어서 줄을 맞춰라](#코드-곳곳을-'열'로-만들어서-줄을-맞춰라)
  3. [의미 있는 순서를 정하여 모든 곳에서 그 순서를 지켜라](#의미-있는-순서를-정하여-모든-곳에서-그-순서를-지켜라)
  4. [빈 줄을 이용하여 커다란 블록을 논리적인 '문단'으로 나누어라](#빈-줄을-이용하여-커다란-블록을-논리적인-'문단'으로-나누어라)

## 여러 블록에 담긴 코드가 모두 비슷한 일을 수행하면, 실루엣이 동일해 보이게 만들어라
 - 일관성과 간결성을 위해서 줄 바꿈을 재정렬하기
    ```java
    // bad
    public class PerformanceTester {
        public static final TopConnectionSimulator wifi = new TcpConnectionSimulator(
            500, /* Kbps */
            80, /* millisecs 대기시간 */
            200, /* 흔들림 */
            1 /* 패킷 손실 % */);
        
        public static final TopConnectionSimulator t3_fiber = 
            new TcpConnectionSimulator(
                45000, /* Kbps */
                10, /* millisecs 대기시간 */
                0, /* 흔들림 */
                0 /* 패킷 손실 % */);

        public static final TopConnectionSimulator cell = new TcpConnectionSimulator(
            100, /* Kbps */
            400, /* millisecs 대기시간 */
            250, /* 흔들림 */
            5 /* 패킷 손실 % */);
    }

    // good
    public class PerformanceTester {
        //     TcpConnectionSimulator (처리량,  지연속도,  흔들림,  패킷_손실)
        //                            [Kbps]   [ms]    [ms]   [percent]

        public static final TopConnectionSimulator wifi = 
            new TcpConnectionSimulator(500,     80,     200,     1);
        public static final TopConnectionSimulator t3_fiber = 
            new TcpConnectionSimulator(45000,   10,     0,       0);
        public static final TopConnectionSimulator cell = 
            new TcpConnectionSimulator(100,     400,    250,     5);
    }
    ```

## 코드 곳곳을 '열'로 만들어서 줄을 맞춰라
- 도움이 된다면 코드의 열을 맞춰라.
    ```python
    CheckFullName("Doug Adams" , "Mr. Douglas Adams" , "");
    CheckFullName("Jake Brown" , "Mr. Jake Brown III", "");
    CheckFullName("No Such Guy", ""                  , "no match found");
    CheckFullName("John"       , ""                  , "more tahn one result");
    ```
    ```python
    details  = request.POST.get('details')
    location = request.POST.get('location')
    phone    = request.POST.get('phone')
    email    = request.POST.get('email')
    url      = request.POST.get('url')
    ```

## 의미 있는 순서를 정하여 모든 곳에서 그 순서를 지켜라
- '가장 중요한 것'에서 시작해서 '가장 덜 중요한 것'까지 순서대로 나열하라.
- 알파벳 순서대로 나열하라.

## 빈 줄을 이용하여 커다란 블록을 논리적인 '문단'으로 나누어라
- 선언문을 블록으로 구성하라
    ```c++
    // bad
    class FrontendServer {
        public:
        FrontendServer();
        void ViewProfile(HttpRequest* request);
        void OpenDatabase(string location, string user);
        void SaveProfile(HttpRequest* request);
        string ExtractQueryParam(HttpRequest* request, string param);
        void ReplyOK(HttpRequest* request, string html);
        void FindFriends(HttpRequest* request);
        void ReplyNotFound(HttpRequest* request, string error);
        void CloseDatabase(string location);
        ~FrontendServer();
    }

    // good
    class FrontendServer {
        public:
            FrontendServer();
            ~FrontendSErver();

        // 핸들러들
        void ViewProfile(HttpRequest* request);
        void SaveProfile(HttpRequest* request);
        void FindFriends(HttpRequest* request);

        // 질의/응답 유틸리티
        string ExtractQueryParam(HttpRequest* request, string param);
        void ReplyOK(HttpRequest* request, string html);
        void ReplyNotFound(HttpRequest* request, string error);

        // 데이터베이스 헬퍼들
        void OpenDatabase(string location, string user);
        void CloseDatabase(string location);
    }
    ```
- 코드를 '문단'으로 쪼개라
    ```python
    # bad
    def suggest_new_friends(user, email_password):
        friends = user.friends()
        friends.emails = set(f.email for f in friends)
        contacts = import_contacts(user.email, email_password)
        contact_emails = set(c.email for c in contacts)
        non_friend_emails = contact_emails - friend_emails
        suggested_friends = User.objects.select(email_in=non_friend_emails)
        display['user'] = user
        display['friends'] = friends
        display['suggested_friends'] = suggested_friends
        return render("suggested_friends.html", display)

    # good 
    def suggest_new_friends(user, email_password):
        # 사용자 친구들의 이메일 주소를 일근ㄴ다.
        friends = user.friends()
        friends.emails = set(f.email for f in friends)

        # 이 사용자의 이메일 계정으로부터 모든 이메일 주소를 읽어들인다.
        contacts = import_contacts(user.email, email_password)
        contact_emails = set(c.email for c in contacts)

        # 아직 치구가 아닌 사용자들을 찾는다.
        non_friend_emails = contact_emails - friend_emails
        suggested_friends = User.objects.select(email_in=non_friend_emails)

        # 사용자 리스트를 화면에 출력한다.
        display['user'] = user
        display['friends'] = friends
        display['suggested_friends'] = suggested_friends
        

        return render("suggested_friends.html", display)
    ```

## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
