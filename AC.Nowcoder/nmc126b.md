

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    for (auto& a: as)
    {
        std::cin >> a;
    }
    std::sort(as.begin(), as.end());
    as.erase(std::unique(as.begin(), as.end()), as.end());

    int max{ as.front() + 8 - as.back() };
    for (int i = 1; i < as.size(); ++i)
    {
        max = std::max(max, as[i] - as[i - 1]);
    }
    int ans{ 8 - max };
    std::cout << ans << '\n';
}
```

