

```c++
void solve()
{
    int a, b, c, n;
    std::cin >> a >> b >> c >> n;
    int ans{ n * a };
    if (n <= b)
        ans -= c;
    std::cout << ans << '\n';
}
```

