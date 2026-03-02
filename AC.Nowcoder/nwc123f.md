

```c++
void solve()
{
    int n;
    std::cin >> n;

    int ans{ 0 };
    std::vector<int> counts(n + 1);
    while (n--)
    {
        int a;
        std::cin >> a;
        if (counts[a - 1] > counts[a])
            --ans;
        ++counts[a];
        if (counts[a] > counts[a + 1])
            ++ans;
        std::cout << ans << ' ';
    }
    std::cout << '\n';
}
```

