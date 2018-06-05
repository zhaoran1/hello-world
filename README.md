/**
 * @desc 生成二维码
 */
private function createRcode($actid = 0)
{
    //生成二维码
    include("application/libraries/phpqrcode.php");
    $path   = FCPATH . "/uploads/rcode/" . date('Y') . '/';  //生成图片存放地址
    mkdirs($path);     //生成文件夹
    $baseEncode = 'http://' . $_SERVER['HTTP_HOST'] . '/active/scancode/'.$actid;   //扫二维码回调地址
    QRcode::png($baseEncode, $path . "$actid.png", 'L', 8, 4);   //调用生成二维码
    $rcode = "/uploads/rcode/" . date('Y') . '/' . "$actid.png";   //入库
    $this->basemodel->update('tao_active_info', array('rcode' => $rcode), array('actid' => $actid));
    return $rcode;
}
