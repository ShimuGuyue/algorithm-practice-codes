

```c++
void solve()
{
    struct Data
    {
        char c;
        int index;

        bool operator<(const Data& o) const
        {
            return this->c < o.c;
        }
        bool operator>(const Data& o) const
        {
            return this->c > o.c;
        }
        bool operator==(const Data& o) const
        {
            return this->c == o.c;
        }
    };

    int n;
    std::cin >> n;
    std::vector<std::pair<int, char>> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> as[i].first >> as[i].second;
    }

    std::vector<std::set<Data>> datas(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        datas[as[i].first].insert({as[i].second, i});
    }

    int count{ 0 };
    std::vector<std::pair<int, int>> ans;
    for (auto& t : datas)
    {
        std::vector<Data> v(t.begin(), t.end());
        for (int i = 0; i + 1 < v.size(); i += 2)
        {
            count += 2;
            ans.push_back({v[i].index, v[i + 1].index});
        }
    }
    std::cout << count << '\n';
    for (auto [a, b] : ans)
    {
        std::cout << a << ' ' << b << '\n';
    }
}
```

