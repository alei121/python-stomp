# python-stomp
The 'S' in STOMP is simple. The stomp.py file includes parsing and writing, is less than 100 lines.

See https://stomp.github.io/ for specification

### Sample usage
```python
import io
from stomp import StompFrame, StompCommand

if __name__ == '__main__':
    # Create new StompFrame
    frame = StompFrame(command=StompCommand.SUBSCRIBE)
    frame.set_header('destination', '/topic/weather')
    frame.set_header('id', '123')
    frame.set_header('content-length', '4')
    frame.set_content('cool')
    
    # Write to output
    s_out = io.StringIO()
    frame.write(s_out)

    # Parse the output back to StompFrame
    s_in = io.StringIO(s_out.getvalue())
    frame = StompFrame.parse(s_in)
    print("content=" + frame.get_content())
```
