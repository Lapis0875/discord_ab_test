# discord_ab_test
ab test utility on discord.py

## Draft
Currently, this project is just on idea stage.

```python
from discord.ext import commands
from ab_test import ABTestManager, TestInfo

ABTest = ABTestManager()    # Class managing all tests

@commands.command(
  name='sample'
)
@ABTest.create_test(name='sample_test', type='shard')    # type : Literal['shard', 'user', 'guild']
async def ab_test_sample(ctx, test_info: TestInfo):
  """
  :param test_info: ab_test.TestInfo object which is injected when rapping command with test.
  """
  if test_info.group == 'A':
    # A group in test
    pass
  elif test_info.group == 'B':
    # B group in test
    pass

@commands.command(
  name='run'
)
async def run_test(ctx, *, test_name: str):
  test = await ABTest.get_test(test_name)
  if test is None:
    return await ctx.send(f'test with name {test_name} does not exist!')
  test.start()
  await ctx.send(f'test started! : {test}')
```
