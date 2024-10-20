https://clickhouse.com/docs/en/install#available-installation-options
https://clickhouse.com/docs/en/architecture/cluster-deployment

create table default.test_table_local ( \
  id Int32, \
  name String, \
  part_mnth Date
) engine = ReplicatedMergeTree( \
  '/clickhouse/all_replicated/tables/0/test_table_local', \
  '0' \
) \
partition by toYYYYMM(part_mnth) \
order by id;

create table default.test_table \
as default.test_table_local \
engine = Distributed