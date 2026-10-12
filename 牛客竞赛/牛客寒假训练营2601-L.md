

```c++
void solve()
{
    int n;
    std::cin >> n;
    for (int i = 1; i <= 10; ++i)
    {
        if (n * i % 10 == 0)
        {
            std::cout << i << '\n';
            return;
        }
    }
}
```

