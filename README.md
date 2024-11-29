# anthropic

## Anthropic Stream Response: 

A- Without Tools 

1- First message comes with type `message_start` This message holds two important info `model` and `usage.input_tokens`

It comes with this format 

```
{
  type: 'message_start',
  message: {
    id: 'msg_bdrk_01GARnYv14iBzB6TkRKGLWRz',
    type: 'message',
    role: 'assistant',
    model: 'claude-3-sonnet-20240229',
    content: [],
    stop_reason: null,
    stop_sequence: null,
    usage: { input_tokens: 288, output_tokens: 1 }
  }
}
```


2- Second chunk `content_block_start` it has no useful information more than indicating that the messages with text as next to this one 

It comes with this format 

```
{
  type: 'content_block_start',
  index: 0,
  content_block: { type: 'text', text: '' }
}
```

3- Third chunk: All the chunks that holds text are same as this one, the important info it holds is the text 

It comes with this format:

```
{
  type: 'content_block_delta',
  index: 0,
  delta: { type: 'text_delta', text: 'Hello' }
}
```

4- At the end of the text chunks, we come to the chunk that has type of `content_block_stop`, it has no useful information except being an indicator that the text chunks has ended. 

it comes with this format

```
{ type: 'content_block_stop', index: 0 }
```

5- After that a chunk with `message_delta` type comes, it holds `stop_reason` which will indicate to the reason that the completion stopped 

```
{
  type: 'message_delta',
  delta: { stop_reason: 'end_turn', stop_sequence: null },
  usage: { output_tokens: 12 }
}
```

6- Last chunk comes with type `message_stop`, it holds some stats about the conversation and most importantly the overall conversation usage

```
{
  type: 'message_stop',
  'amazon-bedrock-invocationMetrics': {
    inputTokenCount: 288,
    outputTokenCount: 12,
    invocationLatency: 1142,
    firstByteLatency: 987
  }
}
```


Summary 

So this is how to extract the data from the chunks

1- model : from the first chunk where chunk.type = ‘message_start’
```js 
const model = chunk.message.model
```

2- message: from the chunks where chunk.type = ‘content_block_delta`
```js 
const message_part = chunk.delta.text
```

3- usage from the last chunk where where chunk.type = ‘message_stop` 

 ```
 js cosnt  inputTokenCount = {chunk.amazon-bedrock-invocationMetric}
```

  ```js
  cosnt  outputTokenCount = {chunk.amazon-bedrock-invocationMetric}
```

