Update Date: 2026.06.24

# 1. Functions that act on rows

1. arrange()
	1. arrange(), unlike sort() (base), NA are sorted to the end.
	2. What is "embracing"? I should consult rlang::args_data_masking
2. distinct()
	1. It is interesting that you can use distinct on computed variables
3. filter() & filter_out()
	1. You should remember that filter() and filter_out() treats NA like FALSE
4. slice(), slice_head(), slice_tail(), slice_min(), slice_max(), slice_sample()
	1. I found nothing to note.

# 2. Functions that act on columns

1. glimpse()
	1. a transposed version of print()
2. mutate()
	1. useful mutate functions:
		1. +, - , log()
		2. lead(), lag()
		3. dense_rank(), min_rank(), percent_rank(), row_number(), cume_dist(), ntile()
		4. cumsum(), cummean(), cummin(), cummax(), cumany(), cumall()
		5. na_if(), coalesce()
		6. if_else(), recode(), case_when()
3. pull()
	1. similar to $, but a nicer look in pipes
4. relocate
	1. I found nothing to note
5. rename() & rename_with()
	1. I found nothing to note
6. select()
	1. : select range of consecutive variables
	2. !complement of a set of variables
	3. & | intersection or union
	4. c() combining selectins
	5. selection helpers
		1. everything()
		2. last_col()
		3. group_cols()
		4. starts_with()
		5. ends_with()
		6. contains()
		7. matches()
		8. num_range()
		9. all_of()
		10. any_of()
		11. where()

# 3. Functions that act on groups of rows

1. count(), tally(), add_count(), add_tally()
	1. I found nothing to note
2. group_by(), ungroup()
	1. I found nothing to note
3. dplyr_by
	1. Use more .by or by rather than group_by
4. rowwise()
	1. I dont't understand what this does. I should try it out.
5. summarise() & summarize()
	1. useful functions
		1. mean() & median()
		2. sd(), IQR(), mad()
		3. min(), max()
		4. first(), last(), nth()
		5. n(), n_distinct()
		6. any(), all()

# 4. Functions that act on data frames

1. bind_cols()
	1. similar to do.call(cbind, dfs)
2. bind_rows()
	1. similar to do.call(rbind, dfs), but output contains all columns that appear in any of the inputs
	2. ".id" parameter is interesting.
3. intersect(), union(), union_all(), setdiff(), setequal(), symdiff()
	1. I found nothing to note.
4. inner_join(), left_join(), right_join(), full_join()
	1. I found nothing to note.
5. nest_join()
	1. I found nothing to note
6. semi_join() & anti_join()
	1. I found nothing to note
7. cross_join()
	1. I found nothing to note
8. join_by()
	1. I found nothing to note
9. rows_insert(), row_append(), rows_update(), rows_patch(), rows_upsert(), rows_delete()
	1. I found nothing to note
# 5. Functions that act on multiple columns

1. across(), if_any(), if_all()
	1. I found nothing to note.
2. c_across()
	1. I found nothing to note.
3. pick()
	1. I found nothing to note.

# 6. Functions that act on vectors

1. between()
2. case_when(), replace_when()
3. coalesce()
4. consecutive_id()
5. cumall(), cumany(), cummean()
6. desc()
7. if_else()
8. lag(), lead()
9. n_district()
10. na_if()
11. near()
12. nth(), first(), last()
13. ntile()
14. order_by()
15. percent_rank(), cume_dist()
16. recode_values(), replace_values()
17. row_number(), min_rank(), dense_rank()
18. when_any(), when_all()