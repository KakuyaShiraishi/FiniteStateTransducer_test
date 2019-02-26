# FiniteStateTransducer_test

Minimal Acyclic Subsequential Transducers を用いたFSTのサンプル


# memo
```cpp
std::vector<std::pair<std::string, uint32_t>> input = {
  { "apr", 30 },
  { "aug", 31 },
  { "dec", 31 },
  { "feb", 28 },
  { "feb", 29 },
  { "jan", 31 },
  { "jul", 31 },
  { "jun", 30 },
};

std::vector<char> t = fst::build(input);

assert(fst::exact_match_search<uint32_t>(t.data(), t.size(), "apr")[0] == 30);
assert(fst::exact_match_search<uint32_t>(t.data(), t.size(), "ap").empty());
assert(fst::exact_match_search<uint32_t>(t.data(), t.size(), "apr_").empty());
assert(fst::exact_match_search<uint32_t>(t.data(), t.size(), "feb")[0] == 28);
assert(fst::exact_match_search<uint32_t>(t.data(), t.size(), "feb")[1] == 29);
```

```cpp
auto t = fst::build<std::string>([](auto add_entry) {
  add_entry("a",       "one");
  add_entry("and",     "two");
  add_entry("android", "three");
});

auto ret = fst::common_prefix_search<std::string>(t.data(), t.size(), "android phone");

assert(ret[0].length == 1);
assert(ret[0].outputs[0] == "one");

assert(ret[1].length == 3);
assert(ret[1].outputs[0] == "two");

assert(ret[2].length == 7);
assert(ret[2].outputs[0] == "three");
```

```cpp
auto t = fst::build({
  "a",
  "and",
  "android",
});

auto ret = fst::common_prefix_search<uint32_t>(t.data(), t.size(), "android phone");

assert(ret[0].length == 1);
assert(ret[0].outputs[0] == 0);

assert(ret[1].length == 3);
assert(ret[1].outputs[0] == 1);

assert(ret[2].length == 7);
assert(ret[2].outputs[0] == 2);
```
