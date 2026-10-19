

```cpp
struct PAM
{
    struct Data
    {
        int count = 0;
        int len   = 0;
        int fail  = 0;
        array<int, 10> nexts = { };
    };

    int last = 0;
    string pattern;
    vector<Data> pam;

    PAM(const string& s)
    {
        pam.assign(2, { });
        pam[0].fail = 1;
        pam[1].len = -1;

        for (char c : s)
        {
            add(c);
        }
        accumulate_count();
    }

    void add(char ch)
    {
        int loc = pattern.size();
        pattern += ch;

        int index = turn(ch);

        int father = get_fail(last, loc, ch);
        if (pam[father].nexts[index] == 0)
        {
            int cur = pam.size();
            pam.emplace_back();
            pam[father].nexts[index] = cur;

            pam[cur].len = pam[father].len + 2;
            if (pam[cur].len == 1)
            {
                pam[cur].fail = 0;
            }
            else
            {
                int fail = get_fail(pam[father].fail, loc, ch);
                pam[cur].fail = pam[fail].nexts[index];
            }
        }

        last = pam[father].nexts[index];
        ++pam[last].count;
    }

    int get_fail(int father, int loc, char ch)
    {
        int fail = father;
        while (!(loc - pam[fail].len - 1 >= 0 && pattern[loc - pam[fail].len - 1] == ch))
        {
            fail = pam[fail].fail;
        }
        return fail;
    }

    void accumulate_count()
    {
        for (int i = pam.size() - 1; i >= 0; --i)
        {
            pam[pam[i].fail].count += pam[i].count;
        }
    }

    int turn(char c)
    {
        return c - '0';
    }
};
```

```cpp
void solve()
{
    int n;
    cin >> n;
    string s;
    cin >> s;

    PAM pam1(s + s), pam2(s);

    auto dfs = [&pam1, &pam2](this auto&& dfs, int x, int y) -> void
    {
        if (x != 0 && x != 1)
            pam1.pam[x].count -= pam2.pam[y].count;

        for (int i = 0; i < 10; ++i)
        {
            if (pam2.pam[y].nexts[i] == 0)
                continue;
            dfs(pam1.pam[x].nexts[i], pam2.pam[y].nexts[i]);
        }
    };

    dfs(0, 0);
    dfs(1, 1);

    int64_t ans = 0;
    int64_t mod = 998'244'353;
    for (auto& [count, len, fail, nexts] : pam1.pam)
    {
        if (len <= 0 || len > n)
            continue;
        ans = (ans + int64_t(count) * count % mod * len % mod) % mod;
    }
    cout << ans << '\n';
}
```

