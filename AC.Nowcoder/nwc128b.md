

```c++
void solve()
{
    std::array<std::pair<int, int>, 3> as;
    for (auto& [a, b] : as)
    {
        std::cin >> a >> b;
    }

    if (as[0].first * 2 == as[1].first + as[2].first &&
        as[0].second * 2 == as[1].second + as[2].second)
        std::cout << 1 << '\n';
    if (as[1].first * 2 == as[0].first + as[2].first &&
        as[1].second * 2 == as[0].second + as[2].second)
        std::cout << 2 << '\n';
    if (as[2].first * 2 == as[1].first + as[0].first &&
        as[2].second * 2 == as[1].second + as[0].second)
        std::cout << 3 << '\n';
}
```

