

```c++
void solve()
{
    int n, a0, a1;
    std::cin >> n >> a0 >> a1;

    std::string ans;

    int64_t flag{ 0 };
    int64_t count0{ 0 }, count1{ 0 };
    for (int i = 0; i < n; ++i)
    {
        int64_t a{ std::llabs((count0 + 1) * a1 - (count1) * a0) };
        int64_t b{ std::llabs((count1 + 1) * a0 - (count0) * a1) };
        if (a <= b)
        {
            ans.push_back('0');
            ++count0;
        }
        else
        {
            ans.push_back('1');
            ++count1;
        }
    }
    std::cout << ans << '\n';
}
```

