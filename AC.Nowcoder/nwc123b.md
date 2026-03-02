

```c++
void solve()
{
    std::array<int, 13> as;
    std::array<int, 13> bs;
    for (auto& a : as)
    {
        std::cin >> a;
    }
    for (auto& b : bs)
    {
        std::cin >> b;
    }

    int ans{ 0 };
    for (int i = 0; i < 13; ++i)
    {
        ans += abs(4 - as[i] - bs[i]);
    }
    ans /= 2;
    std::cout << ans << '\n';
}
```

