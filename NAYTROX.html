// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

abstract contract Context {
    function _msgSender() internal view virtual returns (address) {
        return msg.sender;
    }
}

abstract contract Ownable is Context {
    address private _owner;

    constructor(address initialOwner) {
        _owner = initialOwner;
    }

    modifier onlyOwner() {
        require(_msgSender() == _owner, "Not the owner");
        _;
    }

    function owner() public view returns (address) {
        return _owner;
    }
}

interface IERC20 {
    function totalSupply() external view returns (uint256);
    function decimals() external view returns (uint8);
    function symbol() external view returns (string memory);
    function name() external view returns (string memory);
    function balanceOf(address account) external view returns (uint256);
    function transfer(address recipient, uint256 amount) external returns (bool);
    function allowance(address owner, address spender) external view returns (uint256);
    function approve(address spender, uint256 amount) external returns (bool);
    function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
}

contract NAYTROX is IERC20, Ownable {
    string private _name = "NAYTROX";
    string private _symbol = "NTX";
    uint8 private _decimals = 18;
    uint256 private _totalSupply;

    uint256 public taxFee = 3;
    uint256 public burnFee = 1;
    uint256 public liquidityFee = 1;

    address public taxWallet;
    mapping(address => uint256) private _balances;
    mapping(address => mapping(address => uint256)) private _allowances;

    constructor() Ownable(msg.sender) {
        uint256 initialSupply = 999_000_000 * 10 ** _decimals;
        _balances[msg.sender] = initialSupply;
        _totalSupply = initialSupply;
        taxWallet = msg.sender;
        emit Transfer(address(0), msg.sender, initialSupply);
    }

    function name() public view override returns (string memory) { return _name; }
    function symbol() public view override returns (string memory) { return _symbol; }
    function decimals() public view override returns (uint8) { return _decimals; }
    function totalSupply() public view override returns (uint256) { return _totalSupply; }
    function balanceOf(address account) public view override returns (uint256) { return _balances[account]; }

    function transfer(address recipient, uint256 amount) public override returns (bool) {
        _transfer(_msgSender(), recipient, amount);
        return true;
    }

    function allowance(address owner_, address spender) public view override returns (uint256) {
        return _allowances[owner_][spender];
    }

    function approve(address spender, uint256 amount) public override returns (bool) {
        _allowances[_msgSender()][spender] = amount;
        emit Approval(_msgSender(), spender, amount);
        return true;
    }

    function transferFrom(address sender, address recipient, uint256 amount) public override returns (bool) {
        uint256 allowed = _allowances[sender][_msgSender()];
        require(allowed >= amount, "Not enough allowance");
        _allowances[sender][_msgSender()] = allowed - amount;
        _transfer(sender, recipient, amount);
        return true;
    }

    function _transfer(address sender, address recipient, uint256 amount) internal {
        require(_balances[sender] >= amount, "Balance too low");

        uint256 taxAmount = (amount * taxFee) / 100;
        uint256 burnAmount = (amount * burnFee) / 100;
        uint256 liquidityAmount = (amount * liquidityFee) / 100;
        uint256 netAmount = amount - taxAmount - burnAmount - liquidityAmount;

        _balances[sender] -= amount;
        _balances[recipient] += netAmount;
        _balances[taxWallet] += taxAmount;
        _balances[address(this)] += liquidityAmount;
        _totalSupply -= burnAmount;

        emit Transfer(sender, recipient, netAmount);
        emit Transfer(sender, taxWallet, taxAmount);
        emit Transfer(sender, address(this), liquidityAmount);
        emit Transfer(sender, address(0), burnAmount);
    }

    function updateFees(uint256 _taxFee, uint256 _burnFee, uint256 _liquidityFee) public onlyOwner {
        require(_taxFee + _burnFee + _liquidityFee <= 10, "Too much fee");
        taxFee = _taxFee;
        burnFee = _burnFee;
        liquidityFee = _liquidityFee;
    }

    function setTaxWallet(address _wallet) public onlyOwner {
        taxWallet = _wallet;
    }
}
