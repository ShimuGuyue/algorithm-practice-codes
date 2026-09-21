

```c++
static constexpr int64_t mod{ 1000000007 };

void solve()
{
    int n;
    std::cin >> n;
    std::vector<std::vector<int>> tree(n + 1);
    for (int i = 1; i < n; ++i)
    {
        int u, v;
        std::cin >> u >> v;
        tree[u].push_back(v);
        tree[v].push_back(u);
    }

    int64_t ans{ 0 };
    auto dfs = [&ans, &tree](auto&& dfs, int u, int last, int count, int64_t p) -> void
    {
        auto size{ static_cast<int64_t>(tree[u].size()) };
        if (u != 1)
            ans = (ans + count * p % mod * inv(size) % mod) % mod;
        for (int v : tree[u])
        {
            if (v == last)
                continue;
            dfs(dfs, v, u, count + 1, p * inv(size) % mod);
        }
    };
    dfs(dfs, 1, 0, 1, 1);
    std::cout << ans << '\n';
}

static int64_t quickpow(int64_t base, int64_t power)
{
    int64_t ans{ 1 };
    while (power)
    {
        if (power & 1)
            ans = ans * base % mod;
        base = base * base % mod;
        power /= 2;
    }
    return ans;
}

static int64_t inv(int64_t n)
{
    return quickpow(n, mod - 2);
}
```

