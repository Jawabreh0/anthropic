# anthropic

## Anthropic Stream Response: 

A- Without Tools 

1- First message comes with type `message_startz` This message holds two important info `model` and `usage`
It comes with this format 
```json
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
