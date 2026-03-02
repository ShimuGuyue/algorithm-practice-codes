

```c++
void solve()
{
    int64_t l, r;
    std::cin >> l >> r;

    if (l == r)
    {
        std::vector<int> ans;
        while (l)
        {
            ans.push_back(l % 10);
            l /= 10;
        }
        std::reverse(ans.begin(), ans.end());
        while (ans.back() == 0)
        {
            ans.pop_back();
        }
        std::reverse(ans.begin(), ans.end());

        for (auto a : ans)
        {
            std::cout << a;
        }
        std::cout << '\n';
        return;
    }

    if (r % 10 == 0)
        --r;

    std::string sl{ std::to_string(l) };
    std::string sr{ std::to_string(r) };

    std::vector<int> ans(sr.length());
    ans[0] = 1;

    int index{ 0 };
    if (sl.length() == sr.length())
    {
        for (int i = 0; i < sr.length(); ++i)
        {
            index = i;
            if (sl[i] != sr[i])
                break;
            ans[i] = sl[i] - '0';
        }
    }

    for (int i = ans.size() - 1; i >= index; --i)
    {
        for (int j = 9; j >= 0; --j)
        {
            if (j == 0 && (i == ans.size() - 1 || i == 0))
                continue;
            ans[i] = j;
            int64_t flag{ 0 };
            for (auto a : ans)
            {
                flag = flag * 10 + a;
            }
            if (flag <= r)
                break;
        }
    }
    std::reverse(ans.begin(), ans.end());
    for (auto a : ans)
    {
        std::cout << a;
    }
    std::cout << '\n';
}
```

