---
layout: post
title:  "JAVA异常处理"
categories: Java
---


定义异常

public class AdminException extends RuntimeException {
	

	private AdminErrData errors;

	public AdminErrData getErrors() {
		return errors;
	}

	public void setErrors(AdminErrData errors) {
		this.errors = errors;
	}
	
	public AdminException(){
		
	}
	
	public AdminException(AdminErrData errors){
		this.errors=errors;
	}

}


异常对象

public class AdminErrData implements Serializable {

	private List<AdminError> errors;

	public List<AdminError> getErrors() {
		if (errors==null){
			errors = new ArrayList<AdminError>();
		}
		return errors;
	}

	public void setErrors(List<AdminError> errors) {
		this.errors = errors;
	}
	
	public void addError(AdminError error) {
		getErrors().add(error);
	}


	public static class AdminError implements Serializable {
		private static final long serialVersionUID = 466500232710993303L;
		
		protected Integer errCode;
		protected String errMsg;

		public Integer getErrCode() {
			return errCode;
		}

		public void setErrCode(Integer errCode) {
			this.errCode = errCode;
		}

		public String getErrMsg() {
			return errMsg;
		}

		public void setErrMsg(String errMsg) {
			this.errMsg = errMsg;
		}

		public AdminError() {

		}

		public AdminError(Integer errCode, String errMsg) {
			this.errCode = errCode;
			this.errMsg = errMsg;
		}
		
		public AdminError(String errMsg) {
			this.errMsg = errMsg;
		}

		@Override
		public String toString() {
			return "AdminError [errCode=" + errCode + ", errMsg=" + errMsg + "]";
		}
	}
}

@ControllerAdvice
public class AdviceController {
	private static Logger logger=LoggerFactory.getLogger(AdviceController.class);
	
	@Resource(name="messageSource")
	private MessageSource messages;
	
	
	@ExceptionHandler(Exception.class)
	@ResponseBody
	public AdminErrData handleException(Exception ex,HttpServletResponse response) {
		logger.error("****************异常..."+ex.getMessage());
		
		// 自定义错误
		if (ex instanceof AdminException ) {
			response.setStatus(601);
			return ((AdminException) ex).getErrors();
		}
		
		// 系统错误
		response.setStatus(500);
		AdminErrData ae = new AdminErrData();
		ae.addError(new AdminError(500, "系统错误！"));
		return ae;
	}
}


在业务逻辑里放入自定义错误
异常错误对象
放入自定义异常 抛出
AOP接住 分类处理



@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = StatelessAuthentication.class)
@WebAppConfiguration
@IntegrationTest("server.port:8181")