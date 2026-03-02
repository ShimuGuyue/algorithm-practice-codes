

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::string a, b;
    std::cin >> a;
    std::cin >> b;

    std::string sa;
    std::string sb;
    int lcm = std::lcm(n, m);
    while (sa.length() < lcm)
    {
        sa += a;
    }
    while (sb.length() < lcm)
    {
        sb += b;
    }

    bool borrow{ sa < sb };

    std::reverse(sa.begin(), sa.end());
    std::reverse(sb.begin(), sb.end());

    std::vector<int> as(lcm);
    std::vector<int> bs(lcm);
    for (int i = 0; i < lcm; ++i)
    {
        as[i] = sa[i] ^ '0';
        bs[i] = sb[i] ^ '0';
    }

    std::vector<int> ans(lcm);
    for (int i = 0; i < lcm; ++i)
    {
        as[i] -= borrow;
        borrow = false;
        if (as[i] < bs[i])
        {
            as[i] += 10;
            borrow = true;
        }
        ans[i] = as[i] - bs[i];
    }
    std::reverse(ans.begin(), ans.end());
    std::cout << lcm << '\n';
    for (auto a : ans)
    {
        std::cout << a;
    }
    std::cout << '\n';
}
```

