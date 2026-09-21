

```c++
void solve()
{
    int n, q;
    std::cin >> n >> q;
    std::vector<int> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> as[i];
    }

    std::vector<int> presums(n + 1);
    std::partial_sum(as.begin(), as.end(), presums.begin());

    while (q--)
    {
        int op;
        std::cin >> op;
        if (op == 1)
        {
            int x;
            std::cin >> x;
            presums[x] = presums[x] - as[x] + as[x + 1];
            std::swap(as[x], as[x + 1]);
        }
        else
        {
            int l, r;
            std::cin >> l >> r;
            std::cout << presums[r] - presums[l - 1] << '\n';
        }
    }
}
```

