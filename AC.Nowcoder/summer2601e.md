

```cpp
void solve()
{
    int n;
    std::cin >> n;

    int64_t ans{ 0 };
    for (int64_t i{ 1 }; i <= n; ++i)
    {
        int64_t a;
        std::cin >> a;
        ans += a * (i - 1);
        ans -= a * (n - i);
    }
    std::cout << ans << '\n';
}
```

