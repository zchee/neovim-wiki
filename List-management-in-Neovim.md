Management of lists (types `list_T` and `listitem_T` from vim) was changed in https://github.com/neovim/neovim/pull/7708/. There is a lint against the "old" usage, but here is a list (pun not intended) of the most important changes:

| Old                   | New        | Comment|
|:----------------------------------------|:------------------:|:----------------:|
|`li->lv_first`|`tv_list_first(li)`||
|`li->lv_last`|`tv_list_last(li)`||
|`(li)->li_next`| `TV_LIST_ITEM_NEXT({list}, li)`|To be avoided if possible, must use list which li belongs to.|
|`(li)->li_prev`| `TV_LIST_ITEM_PREV({list}, li)`|To be avoided if possible, must use list which li belongs to.|
|`li->lv_len` | `tv_list_len(li)`||
|`li->lv_lock` |`tv_list_locked(li)`||
|`&li->li_tv` | `TV_LIST_ITEM_TV(li)`||
|`li->lv_refcount++`|`tv_list_ref(li)`||
|`val = li->lv_copyID` | `val = tv_list_copyid(li)`||
|`li->lv_copyID = val`| `tv_list_set_copyid(li, val)`||
|`for (li = list->lv_first; li != NULL; li = li->li_next) { use(li);}`|`TV_LIST_ITER_CONST(list, li, {use(li);})`| If you don't need to modify `li`|
|`for (li = list->lv_first; li != NULL; li = li->li_next) { use(li);}`|`TV_LIST_ITER(list, li, {use(li);})`| Only if you need to modify `li`|




For more details and some more advanced usage, see [`typval.h`](https://github.com/neovim/neovim/blob/master/src/nvim/eval/typval.h#L164) from line 164, [`typeval.c`](https://github.com/neovim/neovim/blob/master/src/nvim/eval/typval.c#L159) from line 159. The line numbers are of commit https://github.com/neovim/neovim/commit/dee78a4095a27369e428572f74f7b64bcc5f670e, so if the links seem strange, try browsing the tree at that point.