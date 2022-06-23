## Describe

convert shared pointer to target pointer

```c
void* tivxMemShared2TargetPtr ( const tivx_shared_mem_ptr_t * shared_ptr )
```

## demo


```c
config_target_ptr = tivxMemShared2TargetPtr(&config_desc->mem_ptr);
```

## supplement

shared pointer 参见 [[c/base/shared_ptr]]