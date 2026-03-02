

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    std::vector<int> bs(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }
    for (auto& b : bs)
    {
        std::cin >> b;
    }

    std::set<int> t;
    t.insert(0);
    for (int i{ 0 }; i < n; ++i)
    {
        std::set<int> temp;
        for (int a : t)
        {
            temp.insert(std::max(a - as[i], 0));
            temp.insert(a ^ bs[i]);
        }
        t = temp;
    }
    int ans{ *t.rbegin() };
    std::cout << ans << '\n';
}
```

