

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> as[i];
    }

    std::vector<int> bs(as.begin() + 1, as.end());
    std::sort(bs.begin(), bs.end());
    bs.erase(std::unique(bs.begin(), bs.end()), bs.end());

    int l;
    int max{ 0 };

    int ll{ 0 }, rr{ 0 };
    int sum{ 0 };
    while (rr < bs.size())
    {
        ++sum;
        while (bs[rr] - bs[ll] + 1 > n)
        {
            ++ll;
            --sum;
        }
        if (sum > max)
        {
            max = sum;
            l = bs[ll];
        }
        ++rr;
    }

    std::map<int, int> counts;
    for (int a : as)
    {
        ++counts[a];
    }

    int flag{ l };
    while (counts[flag] > 0)
    {
        ++flag;
    }
    std::vector<std::pair<int, int>> ans;
    for (int i = 1; i <= n; ++i)
    {
        if (as[i] < l || as[i] > l + n - 1)
        {
            ans.push_back({i, flag++});
            while (counts[flag] > 0)
            {
                ++flag;
            }
        }
        else if (counts[as[i]] > 1)
        {
            --counts[as[i]];
            ans.push_back({i, flag++});
            while (counts[flag] > 0)
            {
                ++flag;
            }
        }
    }
    std::cout << ans.size() << '\n';
    for (auto [a, b] : ans)
    {
        std::cout << a << ' ' << b << '\n';
    }
}
```

