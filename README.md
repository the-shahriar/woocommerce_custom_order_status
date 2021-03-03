# woocommerce_custom_order_status

add_filter( 'bulk_actions-edit-shop_order', 'newoprocessed_dropdown_bulk_actions_shop_order');
function newoprocessed_dropdown_bulk_actions_shop_order( $actions ) {
    $actions['mark_oprocessed'] = __( 'Change status to Order Processed', 'woocommerce' );
    return $actions;
}function register_oprocessed_order_status() {register_post_status( 'wc-oprocessed', array(
        'label'                     => 'Order Processed ',
        'public'                    => true,
        'exclude_from_search'       => false,
        'show_in_admin_all_list'    => true,
        'show_in_admin_status_list' => true,
        'label_count'               => _n_noop( 'Order Processed  <span class="count">(%s)</span>', 'Order Processed  <span class="count">(%s)</span>' )) );}
add_action( 'init', 'register_oprocessed_order_status' );
function add_oprocessed_order_statuses( $order_statuses ) {
    $new_order_statuses = array();foreach ( $order_statuses as $key => $status ) {
        $new_order_statuses[ $key ] = $status;
        if ( 'wc-processing' === $key ) {
            $new_order_statuses['wc-oprocessed'] = 'Order Processed ';}}return $new_order_statuses;}add_filter( 'wc_order_statuses', 'add_oprocessed_order_statuses' );
