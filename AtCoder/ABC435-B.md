

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    for (auto &a : as)
    {
        std::cin >> a;
    }

    int ans{ 0 };
    for (int l = 0; l < n; ++l)
    {
        for (int r = l; r < n; ++r)
        {
            int sum{ 0 };
            for (int i = l; i <= r; ++i)
            {
                sum += as[i];
            }
            bool ok{ true };
            for (int i = l ; i <= r; ++i)
            {
                if (sum % as[i] == 0)
                    ok = false;
            }
            ans += ok;
        }
    }
    std::cout << ans << '\n';
}
```

