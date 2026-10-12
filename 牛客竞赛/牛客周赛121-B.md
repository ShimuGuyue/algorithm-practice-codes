

```c++
void solve()
{
    int n, x;
    std::cin >> n >> x;
    std::vector<int> as(n);
    for (int &a : as)
    {
        std::cin >> a;
    }

    std::vector<int> bs(n + 1);
    for (int i = 0; i < n; ++i)
    {
        if (as[i] + bs[i] < x)
        {
            std::cout << "No\n";
            return;
        }
        if (x <= bs[i])
        {
            bs[i] -= x;
            bs[i + 1] += as[i];
            as[i] = 0;
        }
        else
        {
            as[i] -= x - bs[i];
            bs[i] = 0;
            bs[i + 1] += as[i];
            as[i] = 0;
        }
    }
    std::cout << "Yes\n";
}
```

