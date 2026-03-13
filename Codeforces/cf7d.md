

```cpp
class StringHash
{
private:
    inline static bool is_init{ false };
    inline static int64_t maxlen_{ 5000000 };
    inline static constexpr int64_t base1_{ 5131111 };
    inline static constexpr int64_t mod1_{ 999999937 };
    inline static std::vector<int64_t> powers1_{ };

private:
    std::vector<int64_t> prehashs1_{ };

public:
    StringHash() = default;

    StringHash(const std::string& s)
    {
        build(s);
    }

public:
    int64_t get_hash(const int l, const int r) const
    {
        int64_t prehash1_l = l ? prehashs1_[l - 1] : 0;
        int64_t prehash1_r = prehashs1_[r];
        int64_t hash1{ mod1(prehash1_r - mod1(prehash1_l * powers1_[r - l + 1])) };
        return hash1;
    }

    void build(const std::string& s)
    {
        if (!is_init)
            init();
        const int n{ static_cast<int>(s.length()) };
        prehashs1_.assign(n, 0);
        for (int i{ 0 }; i < n; ++i)
        {
            if (i)
            {
                prehashs1_[i] = mod1(prehashs1_[i - 1] * base1_);
            }
            prehashs1_[i] = mod1(prehashs1_[i] + turn(s[i]));
        }
    }

    void push_back(const std::string& s)
    {
        for (const char c : s)
        {
            push_back(c);
        }
    }

    void push_back(const char c)
    {
        int i{ static_cast<int>(prehashs1_.size()) };
        prehashs1_.emplace_back();
        if (i)
        {
            prehashs1_[i] = mod1(prehashs1_[i - 1] * base1_);
        }
        prehashs1_[i] = mod1(prehashs1_[i] + turn(c));
    }

private:
    static void init()
    {
        is_init = true;
        powers1_.assign(maxlen_, 1);
        for (int i{ 1 }; i < maxlen_; ++i)
        {
            powers1_[i] = mod1(powers1_[i - 1] * base1_);
        }
    }

    static int64_t turn(const char c)
    {
        if (std::islower(c))
            return 411 + c - 'a';
        if (std::isupper(c))
            return 513 + c - 'A';
        if (std::isdigit(c))
            return 821 + c - '0';
        return 1111 + c;
    }

    static int64_t mod1(const int64_t x)
    {
        return (x % mod1_ + mod1_) % mod1_;
    }
};
```

```cpp
void solve()
{
    std::string s;
    std::cin >> s;

    std::string t{ s };
    std::reverse(t.begin(), t.end());

    s = " " + s;
    t = " " + t;

    StringHash sh1(s);
    StringHash sh2(t);

    auto n{ static_cast<int>(s.length()) - 1 };
    int64_t ans{ 0 };
    std::vector<int> dp(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        if (sh1.get_hash(1, i) != sh2.get_hash(n - i + 1, n))
            continue;
        dp[i] = dp[i / 2] + 1;
        ans += dp[i];
    }
    std::cout << ans << '\n';
}
```

