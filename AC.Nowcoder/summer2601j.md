

```cpp
std::vector<std::string> flags;

void init()
{
    for (int i{ 2 }; i <= 14; ++i)
    {
        for (char c : { 'C', 'D', 'H', 'S' })
        {
            flags.push_back(std::string{ turn(i), c });
        }
    }
}
```

```cpp
void solve()
{
    std::array<std::string, 4> as;
    std::array<std::string, 4> bs;
    for (int i{ 0 }; i < 4; ++i)
    {
        std::cin >> as[i];
    }
    for (int i{ 0 }; i < 4; ++i)
    {
        std::cin >> bs[i];
    }

    std::sort(as.begin(), as.begin() + 4, cmp);
    std::sort(bs.begin(), bs.begin() + 4, cmp);

    std::array<bool, 52> visited{ };
    for (int i{ 0 }; i < 4; ++i)
    {
        visited[turn(as[i])] = true;
        visited[turn(bs[i])] = true;
    }

    std::array<std::string, 5> as_cur;
    std::array<std::string, 5> bs_cur;

    int ans{ 1 };   // 1 必赢 0 平局 -1 必输
    for (std::string& s : flags)
    {
        if (visited[turn(s)])
            continue;
        insert(bs, bs_cur, s);
        visited[turn(s)] = true;
        int cur{ -1 };
        for (std::string& t : flags)
        {
            if (visited[turn(t)])
                continue;
            insert(as, as_cur, t);
            cur = std::max(cur, compare(as_cur, bs_cur));
        }
        ans = std::min(ans, cur);
        visited[turn(s)] = false;
    }
    std::cout << ( ans == 1 ? "WoYaoYanPai" : ans == 0 ? "PaiMeiYouWenTi" : "GeiWoCaPiXie") << '\n';
}

void insert(std::array<std::string, 4>& four, std::array<std::string, 5>& five, std::string& s)
{
    int pos{ 0 };
    int a{ turn(s[0]) };
    while (pos < 4 && turn(four[pos][0]) < a)
    {
        ++pos;
    }
    five[pos] = s;
    for (int i{ 0 }; i < 4; ++i)
    {
        if (i < pos)
            five[i] = four[i];
        else
            five[i + 1] = four[i];
    }
}

static bool cmp(const std::string& a, const std::string& b)
{
    return turn(a[0]) < turn(b[0]);
};

auto compare(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    int va{ value(as) }, vb{ value(bs) };
    if (va != vb)
        return va > vb ? 1 : -1;
    return va == 1 ? compare_normal(as, bs)
        :  va == 2 ? compare_1dui(as, bs)
        :  va == 3 ? compare_2dui(as, bs)
        :  va == 4 ? compare_3tiao(as, bs)
        :  va == 5 ? compare_shunzi(as, bs)
        :  va == 6 ? compare_tonghua(as, bs)
        :  va == 7 ? compare_hulu(as, bs)
        :  va == 8 ? compare_4tiao(as, bs)
        :  va == 9 ? compare_tonghuashun(as, bs)
        :  compare_supertonghuashun(as, bs);
}

auto compare_supertonghuashun(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    return 0;
}

auto compare_tonghuashun(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    return compare_shunzi(as, bs);
}

auto compare_4tiao(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    int a{ as[0][0] == as[1][0] ? turn(as[0][0]) : turn(as[4][0]) };
    int b{ bs[0][0] == bs[1][0] ? turn(bs[0][0]) : turn(bs[4][0]) };
    return a > b ? 1 : -1;
}

auto compare_hulu(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    return compare_3tiao(as, bs);
}

auto compare_tonghua(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    return compare_normal(as, bs);
}

auto compare_shunzi(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    int a{ as[4][0] == 'A' ? as[0][0] == '2' ? 5 : turn('A') : turn(as[4][0]) };
    int b{ bs[4][0] == 'A' ? bs[0][0] == '2' ? 5 : turn('A') : turn(bs[4][0]) };
    return a > b ? 1
        :  a < b ? -1
        :  0;
}

auto compare_3tiao(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    int a{ turn(as[2][0]) };
    int b{ turn(bs[2][0]) };
    return a > b ? 1 : -1;
}

auto compare_2dui(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    int ia, ib;
    for (int i{ 0 }; i < 5; ++i)
    {
        if (!(i != 0 && as[i][0] == as[i - 1][0]) && !(i != 4 && as[i][0] == as[i + 1][0]))
            ia = i;
        if (!(i != 0 && bs[i][0] == bs[i - 1][0]) && !(i != 4 && bs[i][0] == bs[i + 1][0]))
            ib = i;
    }
    std::array<int, 3> vas;
    std::array<int, 3> vbs;
    if (ia == 0)
        vas = { turn(as[4][0]), turn(as[2][0]), turn(as[0][0]) };
    else if (ia == 2)
        vas = { turn(as[4][0]), turn(as[1][0]), turn(as[2][0]) };
    else if (ia == 4)
        vas = { turn(as[3][0]), turn(as[1][0]), turn(as[4][0]) };
    if (ib == 0)
        vbs = { turn(bs[4][0]), turn(bs[2][0]), turn(bs[0][0]) };
    else if (ib == 2)
        vbs = { turn(bs[4][0]), turn(bs[1][0]), turn(bs[2][0]) };
    else if (ib == 4)
        vbs = { turn(bs[3][0]), turn(bs[1][0]), turn(bs[4][0]) };
    for (int i{ 0 }; i < 3; ++i)
    {
        if (vas[i] == vbs[i])
            continue;
        if (vas[i] > vbs[i])
            return 1;
        if (vas[i] < vbs[i])
            return -1;
    }
    return 0;
}

auto compare_1dui(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    int ia, ib;
    for (int i{ 1 }; i < 5; ++i)
    {
        if (as[i][0] == as[i - 1][0])
            ia = i;
        if (bs[i][0] == bs[i - 1][0])
            ib = i;
    }
    std::array<int, 4> vas;
    std::array<int, 4> vbs;
    if (ia == 1)
        vas = { turn(as[1][0]), turn(as[4][0]), turn(as[3][0]), turn(as[2][0]) };
    else if (ia == 2)
        vas = { turn(as[2][0]), turn(as[4][0]), turn(as[3][0]), turn(as[0][0]) };
    else if (ia == 3)
        vas = { turn(as[3][0]), turn(as[4][0]), turn(as[1][0]), turn(as[0][0]) };
    else if (ia == 4)
        vas = { turn(as[4][0]), turn(as[2][0]), turn(as[1][0]), turn(as[0][0]) };
    if (ib == 1)
        vbs = { turn(bs[1][0]), turn(bs[4][0]), turn(bs[3][0]), turn(bs[2][0]) };
    else if (ib == 2)
        vbs = { turn(bs[2][0]), turn(bs[4][0]), turn(bs[3][0]), turn(bs[0][0]) };
    else if (ib == 3)
        vbs = { turn(bs[3][0]), turn(bs[4][0]), turn(bs[1][0]), turn(bs[0][0]) };
    else if (ib == 4)
        vbs = { turn(bs[4][0]), turn(bs[2][0]), turn(bs[1][0]), turn(bs[0][0]) };
    for (int i{ 0 }; i < 4; ++i)
    {
        if (vas[i] == vbs[i])
            continue;
        if (vas[i] > vbs[i])
            return 1;
        if (vas[i] < vbs[i])
            return -1;
    }
    return 0;
}

auto compare_normal(std::array<std::string, 5>& as, std::array<std::string, 5>& bs) -> int
{
    std::array<int, 5> vas;
    std::array<int, 5> vbs;
    for (int i{ 0 }; i < 5; ++i)
    {
        vas[i] = turn(as[i][0]);
        vbs[i] = turn(bs[i][0]);
    }
    for (int i{ 4 }; i >= 0; --i)
    {
        if (vas[i] == vbs[i])
            continue;
        if (vas[i] > vbs[i])
            return 1;
        if (vas[i] < vbs[i])
            return -1;
    }
    return 0;
}

auto value(std::array<std::string, 5>& arr) -> int
{
    // 同花顺
    if (judge_tonghua(arr) && judge_shunzi(arr))
        // 皇家同花顺
        if (arr[0][0] == 'T' && arr[1][0] == 'J' && arr[2][0] == 'Q' && arr[3][0] == 'K' && arr[4][0] == 'A')
            return 10;
        else
            return 9;
    // 四条
    if (judge_4tiao(arr))
        return 8;
    // 葫芦
    if (judge_hulu(arr))
        return 7;
    // 同花
    if (judge_tonghua(arr))
        return 6;
    // 顺子
    if (judge_shunzi(arr))
        return 5;
    // 三条
    if (judge_3tiao(arr))
        return 4;
    // 两对
    if (judge_2dui(arr))
        return 3;
    // 一对
    if (judge_1dui(arr))
        return 2;
    // 单张
    return 1;
}

auto judge_tonghua(std::array<std::string, 5>& arr) -> bool
{
    return arr[0][1] == arr[1][1]
        && arr[0][1] == arr[2][1]
        && arr[0][1] == arr[3][1]
        && arr[0][1] == arr[4][1];
}

auto judge_shunzi(std::array<std::string, 5>& arr) -> bool
{
    std::array<int, 5> as;
    for (int i{ 0 }; i < 5; ++i)
    {
        as[i] = turn(arr[i][0]);
    }
    return (as[1] == as[0] + 1 && as[2] == as[1] + 1 && as[3] == as[2] + 1 && as[4] == as[3] + 1)
        || (as[4] == 14 && as[0] == 2 && as[1] == 3 && as[2] == 4 && as[3] == 5);
}

auto judge_4tiao(std::array<std::string, 5>& arr) -> bool
{
    return (arr[0][0] == arr[1][0] && arr[0][0] == arr[2][0] && arr[0][0] == arr[3][0])
        || (arr[4][0] == arr[1][0] && arr[4][0] == arr[2][0] && arr[4][0] == arr[3][0]);
}

auto judge_hulu(std::array<std::string, 5>& arr) -> bool
{
    return (arr[0][0] == arr[1][0] && arr[0][0] == arr[2][0] && arr[3][0] == arr[4][0])
        || (arr[4][0] == arr[2][0] && arr[4][0] == arr[3][0] && arr[0][0] == arr[1][0]);
}

auto judge_3tiao(std::array<std::string, 5>& arr) -> bool
{
    return (arr[0][0] == arr[1][0] && arr[0][0] == arr[2][0])
        || (arr[1][0] == arr[2][0] && arr[1][0] == arr[3][0])
        || (arr[2][0] == arr[3][0] && arr[2][0] == arr[4][0]);
}

auto judge_2dui(std::array<std::string, 5>& arr) -> bool
{
    return (arr[0][0] == arr[1][0] && arr[2][0] == arr[3][0])
        || (arr[0][0] == arr[1][0] && arr[3][0] == arr[4][0])
        || (arr[1][0] == arr[2][0] && arr[3][0] == arr[4][0]);
}

auto judge_1dui(std::array<std::string, 5>& arr) -> bool
{
    return arr[0][0] == arr[1][0]
        || arr[1][0] == arr[2][0]
        || arr[2][0] == arr[3][0]
        || arr[3][0] == arr[4][0];
}

auto static turn(char c) -> int
{
    return c == 'A' ? 14
        :  c == 'K' ? 13
        :  c == 'Q' ? 12
        :  c == 'J' ? 11
        :  c == 'T' ? 10
        :  c - '0';
}

auto static turn(int a) -> char
{
    return a < 10 ? a + '0'
        :  a == 10 ? 'T'
        :  a == 11 ? 'J'
        :  a == 12 ? 'Q'
        :  a == 13 ? 'K'
        : 'A';
}

auto static turn(std::string& s) -> int
{
    int a{ s[1] == 'C' ? 0
        :  s[1] == 'D' ? 1
        :  s[1] == 'H' ? 2
        : 3
    };
    int b{ turn(s[0]) - 2 };
    return a * 13 + b;
}
```

