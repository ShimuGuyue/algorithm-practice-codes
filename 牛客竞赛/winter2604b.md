

```c++
void solve()
{
    int64_t n, q, s;
    std::cin >> n >> q >> s;
    std::vector<int64_t> ts(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> ts[i];
    }

    std::vector<int64_t> begins(n + 1);
    begins[1] = s;
    for (int i = 2; i <= n; ++i)
    {
        begins[i] = begins[i - 1] + ts[i - 1];
    }
    while (q--)
    {
        int x, y;
        std::cin >> x >> y;
        std::cout << begins[x] + y - 1 << '\n';
    }
}
```

