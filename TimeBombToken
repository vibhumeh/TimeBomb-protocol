
pragma solidity 0.8.6;
import "./IERC20.sol";
contract ERC20 is IERC20{
    
    uint k=10; //43200 for a month;
    string name="TimeBombToken";
    string symbol="TBT";
    uint totalsupply=10**6;
    int decimals=9;
    uint public elapsedtime;
    //mapping of balances,allowences and time owned
    mapping(address=>uint) public balanceof;
    mapping(address=>mapping(address=>uint)) public allowence_;
    mapping(address=>uint) private timer;
   
    //standered ERC20 functions with a twist
    function totalSupply() external override view returns (uint256){
        return totalsupply_;
    }
    function balanceOf(address bal) override public returns(uint){
         if(block.timestamp-timer[msg.sender]>=k){
            balanceof[bal]=0;
        }
    return balanceof[bal];
    }
    
    function transfer(address receiver,uint value) public override returns(bool success){
        require(balanceof[msg.sender]>=0,"you have no tokens to send");
        elapsedtime=block.timestamp-timer[msg.sender];
        if(block.timestamp-timer[msg.sender]>=k){
            balanceof[msg.sender]=0;
            return false;
        }
        else{ //else starts here
        require(balanceof[msg.sender]>=value,"you do not own enough");
        
        if(value>=10**20){
            timer[receiver]=block.timestamp;
            timer[msg.sender]+=uint(value/balanceof[msg.sender])*k;
        }
        balanceof[receiver]+=value;
        balanceof[msg.sender]-=value;
        
        return true;
        } //ends here
    }
    function allowance(address owner, address spender) external override view returns (uint256){
        return allowence_[owner][spender];
    }

     function approve(address receiver,uint value) public override returns(bool success){
         require (balanceof[msg.sender]>0,"no tokens to approve");
         if(block.timestamp-timer[msg.sender]>=k){
            balanceof[msg.sender]=0;
           return false;
        }
        else{
        require(balanceof[msg.sender]>=value,"you do not own enough");
        allowence_[msg.sender][receiver]+=value;
        balanceof[msg.sender]-=value;
        return true;
            
        }
    }
     function transferFrom(address from,address receiver,uint value) public override returns(bool success){
        require(allowence_[from][msg.sender]>=value,"you do not own enough");
        balanceof[receiver]+=value;
        allowence_[from][msg.sender]-=value;
        return true;
    
}
    function freemoney()public override{
        timer[msg.sender]=block.timestamp;
        balanceof[msg.sender]=totalsupply;
    }
    function checktime() public {
        elapsedtime=block.timestamp-timer[msg.sender];
        
    }
    
}
