

```cpp
void solve()
{
    int n, k, x;
    std::cin >> n >> k >> x;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    int dif{ as[k] - x };
    for (auto& a : as)
    {
        a = (a - dif + n) % n;
    }

    for (auto a : as)
    {
        std::cout << a << ' ';
    }
    std::cout << '\n';
}
```

