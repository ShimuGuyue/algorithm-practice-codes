

```c++
void solve()
{
    std::string s;
    std::cin >> s;

    int n{ int(s.length()) };
    s += "-";

    std::vector<int> indexs;
    for (int i = 0; i < n; ++i)
    {
        if (s[i] == '1')
            indexs.push_back(i);
    }

    int l{ 0 }, r{ int(indexs.size()) - 1 };
    if (indexs.size() % 2 == 0)
    {
        while (l < r)
        {
            int ll{ indexs[l] };
            int rr{ indexs[r] };
            s[ll] = '-';
            s[rr] = '2';
            ++l;
            --r;
        }
    }
    else
    {
        int loc{ -1 };
        for (int i = 0; i < n; ++i)
        {
            if (s[i] == '1' && s[i + 1] == '2')
            {
                loc = i;
                break;
            }
        }
        if (loc == -1)
        {
            while (l < r)
            {
                int ll{ indexs[l] };
                int rr{ indexs[r] };
                s[ll] = '-';
                s[rr] = '2';
                ++l;
                --r;
            }
        }
        else
        {
            bool find{ false };
            while (l < r)
            {
                int ll{ indexs[l] };
                int rr{ indexs[r] };
                if (!find)
                {
                    if (ll == loc)
                    {
                        ++l;
                        find = true;
                        continue;
                    }
                }
                s[ll] = '-';
                s[rr] = '2';
                ++l;
                --r;
            }
        }
    }

    for (char c : s)
    {
        if (c != '-')
            std::cout << c;
    }
    std::cout << '\n';
}
```

