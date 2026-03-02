

```c++
void solve()
{
    int64_t a, b, c, d, e, f;
    std::cin >> a >> b >> c >> d >> e >> f;
    if ((a - c) * (a - c) + (b - d) * (b - d) == (a - e) * (a - e) + (b - f) * (b - f) &&
        (b - e) * (b - e) + (d - f) * (d - f) == (a - e) * (a - e) + (b - f) * (b - f))
        std::cout << "YES\n";
    else
        std::cout << "NO\n";
}
```

