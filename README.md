# FiniteStateTransducer_test

Minimal Acyclic Subsequential Transducers を用いたFSTのサンプル

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
