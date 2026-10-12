

```cpp
void solve()
{
    int k;
    std::cin >> k;
    double a, b, c, d;
    std::cin >> a >> b >> c >> d;

    double x{ std::max(a, c) + k - std::min(a, c) };
    double y{ std::max(b, d) + k - std::min(b, d) };

    double ans{ x * y - (x - k) * (y - k) };
    std::cout << std::fixed << std::setprecision(10) << ans << '\n';
}
```

