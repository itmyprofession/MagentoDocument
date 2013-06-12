MagentoDocument
===============

Magento Document

Cart Information:

Get all items information in cart

// $items = Mage::getModel('checkout/cart')->getQuote()->getAllItems();
$items = Mage::getSingleton('checkout/session')->getQuote()->getAllItems();
 
foreach($items as $item) {
    echo 'ID: '.$item->getProductId().'<br />';
    echo 'Name: '.$item->getName().'<br />';
    echo 'Sku: '.$item->getSku().'<br />';
    echo 'Quantity: '.$item->getQty().'<br />';
    echo 'Price: '.$item->getPrice().'<br />';
    echo "<br />";           
}
Get total items and total quantity in cart

$totalItems = Mage::getModel('checkout/cart')->getQuote()->getItemsCount();
$totalQuantity = Mage::getModel('checkout/cart')->getQuote()->getItemsQty();
Get subtotal and grand total price of cart

$subTotal = Mage::getModel('checkout/cart')->getQuote()->getSubtotal();
$grandTotal = Mage::getModel('checkout/cart')->getQuote()->getGrandTotal();
- See more at: http://blog.chapagain.com.np/magento-get-all-shopping-cart-items-and-totals/#sthash.IpF6DE1V.dpuf
