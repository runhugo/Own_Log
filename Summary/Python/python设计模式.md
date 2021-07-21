## 1. 单例模式
```
class Singleton:
    def __new__(cls, *args, **kwargs):
        print("获取实例")
        if not hasattr(cls, '_instance'):
            cls._instance = super(Singleton, cls).__init__(cls, *args, **kwargs)
        return cls._instance
```