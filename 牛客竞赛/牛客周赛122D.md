

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

    std::sort(as.begin(), as.end());

    int ans{ n };
    int sum{ 0 };
    for (auto a : as)
    {
        if (a > sum + 1)
            break;
        sum += a;
        if (a != 0)
            --ans;
    }
    std::cout << ans << '\n';
}
```

