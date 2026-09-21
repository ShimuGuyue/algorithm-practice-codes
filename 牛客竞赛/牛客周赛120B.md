

```c++
void solve()
{
    int l, r;
    std::cin >> l >> r;
    int countl = ceilDiv(l, 3);
    int countr = r / 3;
    std::array<int, 3> ans{};
    for (auto &a : ans)
    {
        a += std::max(countr - countl, 0);
    }
    for (int i = l; i <= countl * 3; ++i)
    {
        ++ans[i % 3];
    }
    for (int i = countr * 3 + 1; i <= r; ++i)
    {
        ++ans[i % 3];
    }
    std::cout << ans[1] << ' ' << ans[2] << ' ' << ans[0] << '\n';
}
```

