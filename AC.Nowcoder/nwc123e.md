

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    std::vector<bool> visited(n + 2);
    int ans{ 0 };
    for (auto a : as)
    {
        visited[a] = true;
        int count{ visited[a - 1] + visited[a + 1] };
        if (count == 0)
            ++ans;
        else if (count == 2)
            --ans;
        std::cout << ans << ' ';
    }
    std::cout << '\n';
}
```

