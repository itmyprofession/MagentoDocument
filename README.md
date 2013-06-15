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

-------------------------------------------------------------------------------------------------------------------
Filter products by Price programmatically.

$html='<div>';
$html .= '
<h4>Price</h4>
<ul class="price_grid">';
$html .= $this->priceHtmlnav($maincategoryId);
$html .='</ul>';

echo $html; 


/*price block html
it took price filter and display in menu*/
public function priceHtmlnav($maincategoryId) {

$html='';
$layer = Mage::getModel('catalog/layer');
$category = Mage::getModel('catalog/category')->load($maincategoryId);
if ($category->getId()) {
$origCategory = $layer->getCurrentCategory();
$layer->setCurrentCategory($category);
}
$attributes = $layer->getFilterableAttributes('price');

foreach ($attributes as $attribute) {
if ($attribute->getAttributeCode() == 'price') {
$filterBlockName = 'catalog/layer_filter_price';
$result = $this->getLayout()->createBlock($filterBlockName)->setLayer($layer)->setAttributeModel($attribute)->init();
foreach($result->getItems() as $option) {
$t=str_replace('<span class="price">', "", $option->getLabel());
$t=str_replace('</span>', "", $t);
$html .='<li><a href="'.$category->getUrl().'?price='.$option->getValue()
.'">'.$t.'</a></li>';

}
}
}

return $html;
}
