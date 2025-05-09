// app/Http/Controllers/OrderController.php
use App\Models\Order;
use Illuminate\Support\Facades\Mail;

class OrderController extends Controller
{
    public function placeOrder(Request $request)
    {
        $order = Order::create($request->all());
        Mail::to($order->email)->send(new OrderPlaced($order));
        return redirect()->route('order.success');
    }
}
