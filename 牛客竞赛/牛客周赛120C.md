

```c++
void solve()
{
    int64_t n, m;
    std::cin >> n >> m;
    if (n > m)
        std::swap(n, m);
    if (n == 1)
    {
        std::cout << 1 << '\n';
        return;
    }
    if (n == 2)
    {
        std::cout << (m + 1) / 2 << '\n';
        return;
    }
    if (n == 3 && m == 3)
    {
        std::cout << 8 << '\n';
        return;
    }
    std::cout << n * m << '\n';
}
```

