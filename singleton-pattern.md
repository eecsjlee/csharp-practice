# Singleton Pattern in C#

## 개요

**싱글톤(Singleton)** 패턴은 클래스의 인스턴스를 오직 하나만 생성하고, 전역에서 해당 인스턴스를 공유하여 사용할 수 있도록 보장하는 디자인 패턴입니다.

주로 **설정 객체**, **로깅 시스템**, **게임 매니저** 등과 같이 **공통된 리소스를 관리**해야 하는 경우에 사용됩니다.

---

## 기본 구현 예시

```csharp
public class Singleton
{
    private static Singleton _instance;

    private Singleton()
    {
        Console.WriteLine("Singleton instance created.");
    }

    public static Singleton Instance
    {
        get
        {
            if (_instance == null)
                _instance = new Singleton();
            return _instance;
        }
    }

    public void SayHello()
    {
        Console.WriteLine("Hello from the Singleton!");
    }
}
```

## 싱글톤(Singleton)이란?

**싱글톤 패턴**은 **어떤 클래스의 인스턴스가 오직 하나만 존재하도록 보장하고**, **어디서든 그 인스턴스에 접근할 수 있도록 하는 디자인 패턴**

## 왜 필요할까?

* **전역 상태 관리**가 필요할 때 (예: 설정 정보, 로그 시스템)
* 여러 곳에서 같은 객체를 **공유해서 써야 할 때**
* **자원 낭비를 막기 위해** 인스턴스를 하나만 생성하고 재사용하고 싶을 때

### 예제 코드

```csharp
public class Singleton
{
    private static Singleton _instance;

    // 외부에서 new로 생성하지 못하게 생성자를 private으로 제한
    private Singleton()
    {
        Console.WriteLine("싱글톤 인스턴스 생성!");
    }

    // 인스턴스를 반환하는 정적 프로퍼티
    public static Singleton Instance
    {
        get
        {
            if (_instance == null)
                _instance = new Singleton();
            return _instance;
        }
    }

    public void SayHello()
    {
        Console.WriteLine("안녕, 나는 유일무이한 싱글톤이야!");
    }
}
```

### 사용법

```csharp
Singleton s1 = Singleton.Instance;
Singleton s2 = Singleton.Instance;

s1.SayHello();

// s1과 s2는 같은 인스턴스다!
Console.WriteLine(object.ReferenceEquals(s1, s2));  // True
```

### 스레드 안전하게 만들기 (Thread-Safe)

싱글톤은 멀티스레드 환경에서 문제가 생길 수 있어. 그럴 땐 **lock을 사용하거나 Lazy<T>를 쓰는 방식**으로 안전하게 만들 수 있음

```csharp
public class ThreadSafeSingleton
{
    private static readonly object _lock = new object();
    private static ThreadSafeSingleton _instance;

    private ThreadSafeSingleton() { }

    public static ThreadSafeSingleton Instance
    {
        get
        {
            lock (_lock)
            {
                if (_instance == null)
                    _instance = new ThreadSafeSingleton();
                return _instance;
            }
        }
    }
}
```

또는 더 간단하게

```csharp
public class LazySingleton
{
    private static readonly Lazy<LazySingleton> _instance =
        new Lazy<LazySingleton>(() => new LazySingleton());

    private LazySingleton() { }

    public static LazySingleton Instance => _instance.Value;
}
```

## 요약

> **싱글톤이란, 프로그램 내에서 오직 하나만 존재하는 인스턴스를 제공하는 패턴**
