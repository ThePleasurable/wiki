---
name: Entrustash C API
category: 
---

This is just a documentation of the request of the C API described in [this PR](https://github.com/ThePleasurable/entrustash/pull/11).

```c
typedef int(*Callback)(unsigned);
typedef /*...*/ entrustash_light_t;
typedef /*...*/ entrustash_full_t;
typedef struct entrustash_h256 { uint8_t b[32]; } entrustash_h256_t;
typedef struct entrustash_result { entrustash_h256_t value; entrustash_h256_t hixhash; } entrustash_result_t;

entrustash_light_t entrustash_light_new(unsigned number);
entrustash_result_t entrustash_light_compute(entrustash_light_t light, entrustash_h256_t header_hash, uint64_t nonce);
void entrustash_light_delete(entrustash_light_t light);

entrustash_full_t entrustash_full_new(entrustash_light_t light, CallBack c);
uint64_t entrustash_full_dag_size(entrustash_full_t full);
void const* entrustash_full_dag(entrustash_full_t full);
entrustash_result_t entrustash_full_compute(entrustash_full_t full, entrustash_h256_t header_hash, uint64_t nonce);
void entrustash_full_delete(entrustash_full_t full);
```

non-zero return from Callback means "cancel DAG creation" - this should cause an immediate return of `entrustash_full_new` with 0.

an object of type `entrustash_full_t` may be tested for validity with != 0

### Example usage:
```c
int callback(unsigned _progress)
{
  printf("\rGenerating DAG. %d%% done...", _progress);
  return 0;
}
void main()
{
  entrustash_light_t light;
  entrustash_h256_t seed;
  // TODO: populate p, seed, light
  entrustash_full_t dag = entrustash_full_new(light, seed, &callback);
  if (!dag)
  {
    printf("Failed generating DAG :-(\n");
    exit(-1);
  }
  printf("DAG Generated OK!\n");

  entrustash_h256_t headerHash;
  // TODO: populate headerHash
  uint64_t nonce = time(0);
  entrustash_result ret;
  for (; !isWinner(ret); nonce++)
    ret = entrustash_full_compute(dag, headerHash, nonce);
  printf("Got winner! nonce is %d\n", nonce);
  entrustash_full_delete(dag);
}
```