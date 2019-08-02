# gxc_contract
gxchain contract code

合约接口
1. mine
用户投注

/* 
 * @playable: true
 * @permission: anyone
 * @param   strbet  逗号分割的浮点数，小数点 5 位之后的直接舍去
 * 限制条件 
 *  + 附带的资产大于 0
 *  + 附带的资产必须等于各矿石投注之和
 *  + 附带的资产必须在 prizepool 中存在
 *     且每种矿石若投注则必须大于等于 bet_limit 中对应的值
 *     该局每种矿石的总投注必须小于等于 total_limit 中对应的值
 *  + 投注区块号在该局前 15 个 (block_num%20<15)
 *
 * 可能存在的问题，目前 GXC 资产都是精度都是 5 (GXC目前不支持创建时设置资产精度)
 * 并且当前，线上版不支持合约获得精度，下一版才支持，所以合约代码假设资产精度是 5
 * 即 floor(parseFloat(strFloat)*1e5) 是对应的带精度的资产金额
 * @example 
 * mine("1,2.00,3.000001,0.4"); // 该资产每种矿石分别投注 1 2 3 0.4 
 */
 
void mine(std::string strbet)

2. issueprize
分批发奖,用户太多的话，一次性发奖可能导致合约执行超时而发奖失败

/*
 * @playable: false
 * @permission: anyone, 合约自动控制开奖，不怕用户作弊，只需要有人调用合约执行开奖和发奖流程
 * @param num 发不超过 num 个用户的奖金(即使用户中奖为0也算一个)，-1 表示发所有可发的
 * 特点，若实发奖的数量为 0， 则返回 ERROR_NO_ERROR, 主动使合约失败
 **/
 
void issueprize(int64_t num)
