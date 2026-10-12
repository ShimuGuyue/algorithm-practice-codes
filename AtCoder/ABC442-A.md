

```c++
void solve()
{
    std::string s;
    std::cin >> s;
    int ans{ 0 };
    for (char c : s)
    {
        if (c == 'i' || c == 'j')
            ++ans;
    }
    std::cout << ans << '\n';
}
```

